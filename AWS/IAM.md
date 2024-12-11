# IAM 정리

IAM(Identity and Access Management)은 AWS 계정 내에서 사용자, 그룹, 역할에 대한 인증 및 권한 부여를 관리하는 글로벌 서비스이다.  
이러한 체계는 최소 권한 원칙을 적용하기에 유용하며, 보안 수준을 높이는 핵심 요소이다.

---

## IAM의 주요 개념

### Root Account  
AWS 계정 생성 시 자동으로 만들어지는 루트 계정은 모든 권한을 지니고 있음. 높은 권한으로 인한 보안 위협을 최소화하기 위해 일상적인 업무에서는 사용해선 안되고 유저를 생성하고 관리할때만 사용해야 한다.

### User와 Group  
User는 조직 내 실제 개인을 의미하고, Group은 이러한 사용자들을 논리적으로 묶는 단위이다. 한 사용자는 여러 그룹에 속할 수 있으며, 그룹 단위로 권한을 관리하면 정책 적용 및 변경이 용이하다.

### Policy  
권한은 JSON 형식으로 정의된다. 아래와 같은 형식으로 액션, 리소스, 조건 등을 세밀하게 제어할 수 있다.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::example-bucket"
    }
  ]
}
```
그룹 또는 역할에 연결하면 사용자가 지정된 범위 내에서만 리소스에 액세스할 수 있다.

### Inline Policy
정책을 그룹이나 역할에 부여한 것이 아닌 사용자에게 직접 부여한 것을 말한다.

## 비밀번호 정책과 MFA

1. 비밀번호 정책을 통해 최소 길이, 문자열 조합, 변경 주기 등을 설정하여 관리할 수 있다.  
**IAM > Access management > Account settings** 에서 변경 가능  

2. **MFA(Multi-Factor Authentication)** 적용을 통해 비밀번호가 유출되더라도 계정 탈취를 어렵게 만들 수 있다.  
**root 게정 이름 클릭(오른쪽 위) > Security credentials > My security credentials** 에서 Assign MFA로 추가 가능  
=> 최대 8개 등록 가능하고 삭제할 수 있음

### MFA 종류
- Virtual MFA device
    - 가상 장치
    - Google Authenticator
    - Authy
- U2F(Universal 2nd Factor) Security Key
    - USB안에 키가 있고 이를 컴퓨터에 연결하면 인증 가능한 구조
    - 단일 키를 사용해 여러 루트나 IAM 사용자 지원
    - YubiKey
- Hardware Key Fob MFA Device
    - 실물 MFA 장치
    - Gemalto
- Hardware Key Fob MFA Device AWS GovCloud(US)
    - 미국 정부 클라우드(AWS GovCloud)를 사용하고 있으면
    - SurePassID사용 가능(실물 장치)

## AWS 접근 방식 (Console, CLI, SDK)

AWS에 접근하는 방법은 크게 세 가지가 있다.

1. **AWS Management Console**: 웹 기반 GUI 방식으로, 비밀번호와 MFA를 활용.
2. **AWS CLI**: 명령줄에서 AWS 서비스에 접근하는 도구로, Access Key를 사용. 
3. **AWS SDK**: 프로그램 코드로 AWS 리소스를 제어할 수 있는 라이브러리 집합으로, 다양한 언어를 지원. Access Key를 사용. AWS CLI도 AWS SDK(Python)을 이용해서 만들었음.

Access Key는 유저ID와 Password와 같은 개념이기 때문에 보안을 철저히 유지하는 것이 중요하다. 다음 CLI 명령어를 통해 자격 증명을 설정할 수 있다.

```bash
aws configure
```
위 명령어를 통해 Access Key, Secret Key, 기본 Region, 출력 형식을 지정할 수 있다.

## AWS CloudShell

**CloudShell**은 AWS 웹 콘솔 내에서 제공되는 브라우저 기반 쉘 환경이다. 별도 환경 설정 없이 CLI를 사용할 수 있으며, 인증 정보가 이미 설정되어 있으므로 편리하다고 판단됨. 다만 지원되는 리전이 제한적이며, 이는 [공식 문서](https://docs.aws.amazon.com/cloudshell/latest/userguide/supported-aws-regions.html)에서 확인할 수 있다.

## IAM Role

**IAM Role**은 AWS 서비스나 애플리케이션이 특정 권한을 얻기 위해 사용한다. 예를 들어, EC2 인스턴스가 S3 버킷에 접근하려면 해당 인스턴스에 역할을 할당하여 필요한 권한을 부여할 수 있다. 이 방식은 Access Key를 코드에 직접 삽입하는 위험을 제거하고, 권한 관리를 더 명확하게 할 수 있다.  
**IAM > Roles(역할) > Create role**

## IAM 보안 도구

### IAM Credential Report (account-level)

계정 내 모든 사용자와 그들의 자격 증명 상태를 CSV로 다운로드하는 보고서를 제공한다. 이를 통해 계정 전반의 보안 상태를 점검할 수 있다.  
**IAM > Credential report(자격 증명 보고서) > 다운로드 csv**

### IAM Access Advisor (user-level)

개별 사용자가 어떤 서비스에 접근하는지, 마지막으로 접근한 시점이 언제였는지 확인할 수 있다. 이를 통해 불필요한 권한을 식별하고 제거하는 과정에 도움이 된다.  
**IAM > Users(사용자) > 유저이름 선택 > Last Accessed 선택**

## 모범 사례

- AWS계정을 설정할 때를 제외하곤 루트 계정 사용하지 않기
- 한명의 AWS 사용자는 한명의 물리적 사용자와 동일하다
    - 다른 사람에게 자격증명정보를 제공하지 말고 새로운 유저를 생성해서 건네주기
- 사용자를 그룹에 할당하고 그룹에 권한을 할당하여 보안이 그룹수준에서 관리되도록 하기
- 강력한 비밀번호 정책 만들기
- MFA사용 강제하기
- AWS서비스에 권한을 부여할때는 Role(역할)을 생성하고 사용하기
    - 프로그래밍 방식이나 EC2내부에서 AWS CLI키를 등록할때도 포함된다
- CLI/SDK를 사용하기 위해 Access Key 만들기
- 계정의 권한을 감사하기 위해 IAM 자격 증명 보고서나 IAM 액세스 관리자 기능을 사용하기
- 절대로 IAM 사용자나 Access Key를 공유해선 안됨
