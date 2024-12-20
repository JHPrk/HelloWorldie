# Apache Kafka Series

# Topic

카프카 토픽은 카프카 클러스터 안에 있는 데이터 스트림을 가르킴

카프카 클러스터에는 많은 토픽이 있을 수 있음

카프카 토픽 = 데이터스트림 

데이터베이스에 제약조건이 없는 테이블을 만드는 것과 비슷한 개념 

- 데이터 검증이 없음 → 원하는건 모두 토픽에 집어넣을 수 있음.

카프카 클러스터안에 원하는 만큼 토픽 생성 가능

이름을 이용해서 토픽을 식별함 (logs, purchases 등)

모든 종류의 메시지 형식을 지원 - JSON, Avro, txt, binary 다 가능

토픽 안에 있는 메시지들의 순서를 데이터 스트림이라고 함

그래서 Kafka를 데이터 스트리밍 플랫폼이라고 함

토픽을 통해 스트림을 만드니까

토픽은 쿼리로 조회 불가

대신에 토픽에 데이터를 추가 가능 → 프로듀서

읽기도 가능 → 컨슈머

Kafka안에는 쿼리기능은 없음

# Partition & Offset

토픽을 파티션들로 분할할 수 있음

- 하나의 토픽을 100개의 파티션으로 구성이 가능
- 각 파티션 안의 메시지들은 순서가 정해짐
- 각 파티션안의 메시지의 id는 0부터 계속 증가하는데 이를 카프카 오프셋이라고 함
- 각 파티션에는 다른 오프셋을 갖고 있음
- 토픽은 immutable임
    - 한번 발행하면 삭제와 업데이트 불가능 기록만 가능

배송 트럭을 기반으로 한 서비스를 예로들어보자

- 각 트럭의 gps 데이터를 보내는 서비스가 있음
- 모든 트럭은 20초를 간격으로 gps데이터를 보냄
- 이 데이터는 truck_gps라는 토픽(데이터 스트림)에 저장됨
- 몇개의 파티션으로 나뉘어져 저장되는데 이 데이터를 여러서비스가 이용함
    - 이 위치 데이터스트림을 가지고 위치 추적을 도와주는 대시보드 생성이 가능
    - 배송이 완료되었으면 알려주는 알림 서비스
- 이렇게 동일한 데이터 스트림을 다수의 서비스가 읽을 수 있다는 장점

## 중요한점

1. 어떤 데이터가 파티션에 기록되면 변경할 수 없음 (불가변성)
2. 카프카 데이터는 일정시간동안만 유지됨 (기본설정 1주일)
    1. 1주일 뒤에는사라짐
3. 오프셋은 특정한 파티션에서만 유효함
    1. 파티션 0의 오프셋 3은 파티션 1의 오프셋3과 다르다 (독립적)
    2. 오프셋은 한번 만들어지면 다시 사용 못함 (앞의 메시지들이 삭제되었어도) 
    3. 메시지를 보내면 계속 1씩 증가함
4. 파티션 안에서만 순서가 보장됨 다른 파티션에는 보장하지 않음
5. 데이터가 만들어지면 해당 데이터는 **키를 제공하지 않는 이상** 임의의 파티션에 할당됨 
6. 카프카 토픽안에는 원하는 만큼의 파티션을 만들 수 있음
    1. 적절한 파티션 수를 결정하는 방법도 있음

### 요약

1. 각 파티션에는 메시지가 있고 오프셋이 순서대로 증가함
2. 오프셋 순서로 읽음
3. 다른 파티션의 메시지는 제어할 수 없음

# Producer

- 데이터를 토픽에 기록하기 위해서 프로듀서가 필요
- 프로듀서는 토픽과 파티션에 데이터를 기록
- 프로듀서는 Kafka 토픽과 파티션에 데이터를 전송
    - 프로듀서는 자신이 어떤 파티션에 기록하는지 알고 있음
- Kafka 브로커, 즉 서버가 그걸 갖게됨
- 따라서 프로듀서는 어떤 파티션에 메시지가 기록될 것인지 미리 알고 있음
    - 서버가 파티션을 결정하는 것이 아님!!
    - 기록할 파티션을 결정하는 것은 프로듀서임
- Kafka 서버에서 어떤 파티션에 장애가 있을 경우 프로듀서가 자동적으로 복구를 수행함
- 프로듀서는 로드밸런싱을 수행함
    - 모든 파티션에 걸쳐 데이터를 전송하기 때문

# Message key

- 프로듀서는 메시지안에 메시지 키를 넣을 수 있음
    - string number binary모두 가능
- 키가 Null이라면 데이터가 round-robin방식으로 전송됨.
    - 파티션 0…n으로 순차적으로 로드밸런싱 수행
- 키가 null이 아니라면?
    - 동일한 키를 공유하는 모든 메시지들은 해싱 전략 덕분에 항상 동일한 파티션에 기록됨(중요)
- 키를 지정할 때 특정 필드에 대한 메시지 순서 설정을 해야 함
- 특정 데이터에 대한 순서 보장이 중요할때는 key값을 활용해서 항상 같은 파티션으로 가도록 하자
    - 어떤키가 어떤 파티션에 속할지는 해싱 기법에 따라  다름.

### Kafka 메시지의 구조

![image.png](Apache%20Kafka%20Series/image.png)

- Key - Value가 binary형태로 들어옴 (nullable)
- Compression Type을 지정해 메시지를 압축할 수 있음 (none도 있음)
- Header도 추가 가능 - Optional이고 key-value 쌍인 리스트
- 파티션과 오프셋 정보
- 타임스탬프 정보

### Kafka Message Serializer

- 카프카는 producer로부터 바이트만 전달 받고 consumer에서 바이트를 전달하는 구조
- 그러나 메시지를 구성할때는 바이트형태가 아니기 때문에 메시지 직렬화를 수행해야함.
- 직렬화 : 데이터나 객체를 바이트로 변환하는 것
- 카프카 직렬화는 value와 key에만 적용됨.
- KeySerializer, ValueSerializer를 서로 다른 형태로 유연하게 지정 가능
    
    ![image.png](Apache%20Kafka%20Series/image%201.png)
    
- 위 변환을 거쳐야 Apache Kafka로 데이터 전송 가능
- Kafka Producer는 기본으로 제공하는 Common Serilizer를 갖고 있음
    - String (JSON 포함)
    - Int, Float
    - Avro
    - Protobut

### Key Hashing

- 카프카 파티셔너라는 코드 로직이 레코드, 즉 메시지를 받아서 전송 대상인 파티션을 결정함
- 메시지를 send하면
    - Producer Partitioner logic이 레코드를 확인하고 파티션을 지정
    - 이 데이터를 받아서 프로듀서가 Kafka에 전송
- 파티션과 키를 매핑하기 위해 사용
- default Partitioner로 murmur2알고리즘을 사용함

```java
targetPartition = Math.abs(Utils.murmur2(keyBytes)) % (numPartitions - 1)
```

- keyBytes를 murmur2 알고리즘을 적용하고 partition 수를 나머지연산하여 타겟 파티션 결정