# 개발자 용어 사전

> 개발자로서 알고 있으면 좋은 용어나 최신 기술들에 대한 사전을 만들면 좋겠다 싶어서 만든 페이지입니다.  
제가 따로 공부를 진행하면서 이미 알고 있는 용어나 잘 모르는 용어들을 리스트 업해서 하나씩 채워나가는 페이지입니다.  
업무를 진행하거나 개발을 진행하면서 헷갈리거나 잘 모르는 용어들에 대해 사전처럼 바로 찾을 수 있을 정도로 작성하고 싶습니다.  
아직 옆에 뜻이 작성되지 않은 단어들은 작업중인 단어들입니다. 용어 수정에 대한 제안은 언제든지 환영합니다.
> 

# A

**Access Control (접근 제어)** : 시스템, 네트워크, 데이터 또는 리소스에 대한 접근 권한을 관리하고 제한하는 보안 메커니즘

**Active-Active Architecture** : 두 개 이상의 노드(서버, 데이터베이스 등)가 동시에 실시간으로 작업을 수행하고 부하를 분산하는 아키텍처

**Active-Passive Architecture** : 주 노드(Active Node)가 실제 작업을 수행하고, 대기 노드(Passive Node)가 백업 상태로 대기하는 아키텍쳐

**Active-Standby Architecture** : Active-Passive 아키텍처를 의미

**API (Application Programming Interface)** : 애플리케이션 간의 상호 작용을 정의하고 데이터 교환을 가능하게 하는 인터페이스

**API-Gateway** : 클라이언트와 백엔드 서비스 간의 중앙 인터페이스 역할을 하는 중개 계층(미들웨어). 클라이언트 요청을 다양한 백엔드 서비스로 라우팅하고, 응답을 조정하여 클라이언트에 반환하는 인프라 구성 요소

**APM (Application Performance Monitoring/Management)** : 애플리케이션의 성능, 가용성, 사용자 경험을 실시간으로 추적하고 관리하는 솔루션

**Application Concern (애플리케이션 우려사항)** : 소프트웨어 설계와 개발 과정에서 중요하게 고려해야 할 사항이나 문제 영역을 의미. 기능적 요구사항/비기능적 요구사항을 모두 포함

**AWS (Amazon Web Services)** : Amazon에서 제공하는 클라우드 컴퓨팅 플랫폼. 전 세계 데이터 센터를 통해 다양한 클라우드 서비스(컴퓨팅, 스토리지, 데이터베이스, AI/ML 등)를 제공

# B

**Backup (백업)** : 데이터 손실에 대비해 원본 데이터를 복사하여 안전한 장소에 저장하는 과정

**Batch (배치)** : 일괄 처리 방식으로, 데이터를 한꺼번에 모아서 처리하는 프로세스

**Business Logic (비지니스 로직)** : 소프트웨어 애플리케이션에서 특정 비즈니스 규칙과 절차를 구현하는 부분

# C

**Cache (캐시)** : 자주 사용되는 데이터나 연산 결과를 임시로 저장하는 고속 데이터 저장소. 데이터 액세스 속도를 향상시키고 시스템 성능을 최적화하기 위해 사용

**Consumer (컨슈머)** : 데이터나 서비스를 소비하는 주체, Producer(생산자)와 상호작용 함

**Consumer Offset (컨슈머 오프셋)** : 메시지 큐 시스템에서 컨슈머가 읽은 메시지의 위치 또는 인덱스

**Coroutines** : 비동기 프로그래밍을 간결하고 효율적으로 관리할 수 있는 Kotlin 언어의 경량 비동기 처리 도구, 스레드 블로킹 없이 작업을 일시 중지(suspend)하고, 비동기 작업을 직관적으로 처리 가능

**CNI (Container Network Interfaces)** : 컨테이너의 IP 주소 할당, 네트워크 연결 생성 및 삭제 작업을 수행하며, 네트워크 플러그인 개발을 위한 오픈 소스 표준 사양

**Calico CNI** : 컨테이너 기반 애플리케이션에서 네트워크 연결과 보안 정책을 관리하는 오픈 소스 네트워킹 및 보안 솔루션, Kubernetes, OpenShift 등 다양한 오케스트레이션 시스템과 통합되어 네트워크 정책 관리, 서비스 메시, 엔드포인트 보안 등을 제공

**Canary (카나리)** : 소프트웨어 배포 전략 중 하나로, 새로운 버전을 점진적으로 배포하여 안정성을 검증하는 방식. 소규모 사용자 그룹에게 먼저 새 버전을 배포하고, 문제가 없으면 점진적으로 전체 시스템으로 확장 

**Ceph** : 오픈 소스 분산 스토리지 시스템으로, 클라우드 환경에서 대규모 데이터 저장소를 구축할 수 있도록 설계됨. 다양한 하드웨어 환경에서 자동화된 데이터 복제 및 복구, 자동 확장, 고속 데이터 액세스 등을 제공

**Circuit Breaker**

**Client-side**

**Cluster**

**Component (컴포넌트)**

**Connection**

**Connection Pool**

**Container**

**Container Orchestration (컨테이너 오케스트레이션)** : 컨테이너 기반 애플리케이션의 자동 배포, 관리, 조정, 확장 및 복구를 수행하는 프로세스, 컨테이너 수명 주기를 관리하고 리소스 최적화, 부하 분산, 장애 복구 등을 자동으로 처리

# **D**

**Data Center (데이터 센터)**

**Data Pipeline**

**DB (Database, 데이터베이스)**

**Dead Letter Queue** 

**Dead Letter Topic** 

**Decryption (복호화)** 

**Delay** 

**Delay Retry Topic** 

**Deploy (배포)** 

**Direct style** 

**DSL** 

**Dualization (이중화)**

**DC/OS**

**Distribute Lock (분산락)**

**DNS**

**dump**

**dynamic**

# **E**

**Ecosystem (생태계)**

**Elasticsearch** 

**Encryption (암호화)** 

**Enqueue** 

**envoy filter** 

**ES (Elasticsearch)**

**ES Alert** 

**ES Log** 

**Event (이벤트)**

**ELK(Elastic Logstatsh Kafka)**

**envoy**

**envoy proxy**

# **F**

**Failure Injection Test** 

**Flink**

**Fallback**

**Filebeat**

# **G**

**Grafana** 

**Gateway** 

**Gateway Routing** 

**Grafana**

# **H**

**HA (High Availability, 고가용성)** : 시스템, 서비스 또는 애플리케이션이 장시간 중단 없이 지속적으로 운영될 수 있도록 보장하는 IT 시스템의 설계 원칙 및 구현 전략

**Hadoop**

**Header**

**Host**

**Http**

# **I**

**I/O** 

**ID** 

**Infrastructure Concern** 

**Instance** 

**iptable** 

**Infrastructure**

**Istio** : 마이크로서비스 간의 통신 관리, 보안, 모니터링 및 트래픽 제어를 위한 오픈 소스 플랫폼. Kubernetes 클러스터 또는 컨테이너 기반 애플리케이션에서 서비스 간 네트워크 트래픽을 관리하고, 정책 제어, 보안 기능 강화, 실시간 모니터링을 지원

**Istio Error Flag** 

**Istio Route Weight**

**Istio-proxy**

# **J**

**Java**

**Jedis**

# **K**

**K8S (Kubernetes)**

**Kafka**

**Kafka Kibana kong**

**Kotlin**

**Kubernetes**

# **L**

**L7 (Layer 7 Switch)**

**Learning Curve** 

**Lettuce** 

**Logstash**

**Lifecycle**

**Loadbalance**

**Loadbalancer**

**Log**

# **M**

**Maintenance (유지보수)** 

**Memcached** 

**Memory** 

**Metric**

**Migration** 

**Module** 

**Monitoring** 

**Monolithic** 

**mTls** 

**MVC** 

**MySQL**

**Memcached**

**Message Queue**

**Monitoring**

**MSA**

# **N**

**Network**

**Node**

# **O**

**Oauth2** 

**Oauth2 Filter** 

**Observability** 

**Open source**

**Optimistic Lock**

# **P**

**Pinpoint** : 오픈 소스 APM 도구, 분산된 시스템과 마이크로서비스 기반 애플리케이션의 성능 모니터링 및 문제 진단을 지원. 서비스 호출 추적, 성능 병목점 분석, 메트릭 수집 등을 수행

**Platform** 

**PR(Pull Request)** 

**Producer** 

**Prometheus**

**Pipeline**

**Proxy** : 클라이언트와 서버 간의 중간 대리자. 클라이언트가 서버에 직접 연결하지 않고 프록시 서버를 통해 요청을 전달하고, 응답을 수신함. 보안 강화, 트래픽 관리, 로드 밸런싱, 콘텐츠 캐싱 등을 수행

# **Q**

**Queue**

# **R**

**R2DBC (Reactive Relational Database Connectivity)** : 관계형 DB에서 reactive programming을 가능하게 해주는 non-blocking 관계형 데이터베이스 접근 표준

**Reactor**

**Reactor Control Flow**

**Reactor Operator**

**Redis**

**Redis Client**

**Redis Cluster**

**Redis Master**

**Redis Slave**

**Redission**

**Redlock** : 다중 Redis 인스턴스로 구성된 분산된 환경에서 락을 안전하게 획득하고 관리하기 위한 분산 락 표준 알고리즘

**Replication**

**Request (요청)**

**Requeue**

**Retry**

**Rollback (롤백)**

**Route53**

**Router**

# **S**

**Sentry**

**Server**

**Server-side**

**Service**

**Service Discovery**

**Service Mesh**

**Sidecar**

**Slack**

**Slot Rebalance**

**Split Brain**

**Spring**

**Spring cloud gateway**

**Squeeze Test**

**Static**

**Static file**

# **T**

**tcpdump**

**Thanos**

**Traffic**

**Transaction Outbox Pattern**

# **U**

# **V**

**Vamp**

# **W**

**Warning**

**WebFlux**

**Wrapping**

# **X**

# **Y**

# **Z**

**Zuul**