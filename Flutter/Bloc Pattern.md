# 플러터의 상태관리

- 플러터는 위젯 기반이기 때문에 모든 것은 상태기반이다.
- 그러나 구현하다보면 부모의 상태가 여러 자식들의 상태에 영향을 미칠때가 있다. 이럴때 필요한 것이 바로 상태관리 도구임.
- 이를 가능케해주는 것이 바로 Bloc 패턴이다.

## BloC Pattern
- UI <-> BloC <-> DATA
- BloC(Business Logic Component)은 플러터의 상태 관리 패턴으로, 비지니스 로직을 UI 위젯과 분리하여 비지니스 로직의 재사용성을 높일 목적으로 만들엇음.
- 위젯은 가능한한 수동적이어야 하며, 비즈니스 로직은 별도의 컴포넌트로 존재해야 한다는 것이 블록 패턴의 핵심 개념

## 블록 패턴 구현하기
- <a href= https://pub.dev/packages/flutter_bloc> <img src="https://github.com/JHPrk/HelloWorldie/assets/23393661/2f2faab9-985e-4ef2-a592-f8d9c5761ff1" width="100"> </a>
<a href= https://pub.dev/packages/equatable> <img src="https://github.com/JHPrk/HelloWorldie/assets/23393661/a8117cdb-d9d1-423c-bab3-08d856740760" width="160"> </a>

- 위 두 패키지를 통해 쉽게 구현할 수 있음

- 블록 패턴을 구현하기 위한 3가지
  - State
  - Event
  - Bloc Provider
- 우선 상태를 정의하고, 그에 따른 이벤트를 정의한 뒤, 각 상태 마다 적용 가능한 비지니스 로직을 구현한다.
