# AWS Global Infrastructure 정리

AWS는 전 세계에 걸쳐 분포한 인프라를 바탕으로 안정적이고 빠른 클라우드 서비스를 제공한다. AWS 인프라를 이해하는 것은 효율적인 아키텍처 설계에 큰 도움이 된다고 한다. 이를 이해하기 위해서 크게 **Region**, **Availability Zone**, **Edge Location**, 그리고 **Global** 및 **Region-Scoped 서비스**에 대해 살펴보도록 하자.

## AWS Global Infrastructure 개요

AWS 인프라 구성의 큰 틀은 **Region(리전)**, **Availability Zone(가용 영역)**, 그리고 **Edge Location(엣지 로케이션)** 으로 나뉜다. 각각은 물리적 또는 논리적 위치로서, 서비스의 지연 시간, 비용, 가용성에 직접적인 영향을 준다.

## Region (리전)

**Region**은 전 세계 여러 위치에 분포된 독립적인 지리적 영역으로서, 여러 개의 데이터센터 집합으로 이루어져 있다. 많은 AWS 서비스들이 Region 단위로 제공되며, 다음과 같은 기준으로 Region을 선택하면 됨.

- **법률 준수**: 각 국가마다 데이터 관리에 대한 법률이 상이. 예를 들어, 고객 데이터가 특정 국가 밖으로 반출되지 않아야 하는 경우 해당 국가에 위치한 Region을 선택.
- **지연 시간**: 물리적으로 가까운 Region일수록 네트워크 레이턴시(지연 시간)가 낮아 빠른 응답 속도를 가짐.
- **사용 가능 서비스 확인**: 원하는 AWS 서비스가 특정 Region에서만 사용 가능한 경우가 있으므로, 서비스 가용 여부를 미리 확인.
- **요금 차이**: 동일한 서비스라도 Region마다 가격이 다름. 예산이나 비용 최적화를 위해 Region을 신중히 선택해야 함.

### 예시 코드 (AWS CLI를 활용한 Region 조회)

```bash
aws ec2 describe-regions --query "Regions[].RegionName" --output table
```

위 명령어를 통해 현재 사용 가능한 모든 EC2 Region 목록을 조회하여 테이블 형태로 출력할 수 있다.

## Availability Zone (AZ)

**Availability Zone(AZ)** 은 하나의 Region 안에 존재하며, 최소 3개 이상, 많게는 6개 이상의 AZ로 구성된다. 각 AZ는 하나 혹은 그 이상의 독립적인 데이터센터로 이루어져 있다고 한다. 이를 통해 특정 AZ에서 문제가 발생하더라도 다른 AZ를 활용할 수 있어 애플리케이션의 가용성을 유지할 수 있다.

AZ들은 높은 대역폭의 저지연 네트워크로 연결되어 있기 때문에 다중 AZ 아키텍처를 손쉽게 구현할 수 있다. 예를 들어, 웹 서버를 서로 다른 두 개의 AZ에 배치하여 한쪽에 장애가 발생해도 다른 쪽을 통해 서비스가 중단 없이 제공되도록 할 수 있다.

### Data Centers

각각의 AZ를 구성하는 실제 물리적 시설이 **데이터 센터(Data Center)** 이다. AWS는 엄격한 보안 및 안정성 표준에 따라 데이터 센터를 운영하여 높은 신뢰성과 보안을 보장한다고 한다.

## Edge Locations / Points of Presence (PoP)

**Edge Location** 또는 **Point of Presence (PoP)** 는  전 세계에 걸쳐 400개 이상 존재하는 콘텐츠 전송 지점이다. CloudFront와 같은 CDN(Content Delivery Network) 서비스를 통해 최종 사용자에게 콘텐츠를 빠르고 안정적으로 전달한다. 사용자는 지리적으로 가까운 Edge Location에서 데이터를 전달받기 때문에 높은 성능을 기대할 수 있다.

## Global Services

**글로벌 서비스(Global Services)** 는 특정 Region에 종속되지 않고 전 세계적으로 동일한 엔드포인트를 통해 사용 가능한 서비스이다. 대표적인 글로벌 서비스는 다음과 같다.

- **IAM(Identity and Access Management)**: 보안 자격증명 관리 및 권한 제어
- **Route 53(DNS)**: 글로벌 DNS 관리 서비스
- **CloudFront(CDN)**: 전 세계 엣지 로케이션을 활용한 콘텐츠 전송
- **WAF(Web Application Firewall)**: 웹 애플리케이션 방화벽 관리 (보안)

이러한 서비스들은 전 지구적 관점에서 애플리케이션과 사용자를 연결하고 보호하기 때문에 특정 Region에 구애받지 않는다..

## Region-Scoped Services

대부분의 AWS 서비스는 특정 Region에 종속적으로 동작하는 **Region-Scoped 서비스**. 

대표적인 예시
- **EC2**: 가상 서버 리소스 제공
- **Elastic Beanstalk**: 애플리케이션 배포 및 관리 플랫폼
- **Lambda**: 서버리스 컴퓨팅 서비스

이러한 서비스들은 자신이 배치된 Region 내에서 리소스를 운영하며, 다른 Region과 물리적으로 분리된다. 따라서 Region 선택 시 서비스 가용성과 특성을 반드시 고려해야 한다.

## 결론
이번 포스팅에서는 AWS Global Infrastructure에 대해 정리해보았다. **Region**, **AZ**, 그리고 **Edge Location** 이 어떻게 서로 유기적으로 연결되어 글로벌 규모의 인프라를 구성하며, 이를 바탕으로 글로벌 서비스와 Region-Scoped 서비스로 나뉘어지는 것을 정리했다.