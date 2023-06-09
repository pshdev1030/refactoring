### 2-1 리팩터링 정의

리팩터링은 소프트웨어의 겉보기 동작은 그대로 유지한 채, 코드를 이해하고 수정하기 쉽도록 내부 구조를 변경하는 기법이다.

### 2-2 두 개의 모자

소프트웨어를 개발할 때의 목적을 기능 추가와 리팩터링 두 가지로 분류하고, 각각을 모자로 정의하였다.

기능추가 할 때는 기능추가만, 리팩터링 할 때는 리팩터링만 해야한다.

### 2-3 리팩터링 하는 이유

리팩터링은 다음과 같은 효과를 가진다.

#### 리팩터링 하면 소프트웨어 설계가 좋아진다.

아키텍쳐를 고려하지 않은 채 단기 목표만을 위해 코드를 수정하면 기반 구조가 무너지기 쉽다.

코드만으로 설계를 파악할 수 있도록 해야한다.

#### 리팩터링 하면 소프트웨어를 이해하기 쉬워진다.

코드에서 의도를 더욱 명확하게 파악할 수 있도록 개선할 수 있다.
코드에 대해서 기억하지 않아도 코드만 보고 의도를 파악할 수 있다.

#### 리팩터링 하면 버그를 쉽게 찾을 수 있다.

코드를 이해하기 쉽다는 말은 버그를 찾기 쉽다는 말이기도 하다.

프로그램 구조를 명확하게 다듬으면 그냥 '이럴 것이다'라고 가정하던 점들이 분명히 들어난다.

#### 리팩터링 하면 프로그래밍 속도를 높일 수 있다.

정리하자면 리팩터링 하면 코드 개발 속도를 높일 수 있다.
새로운 기능을 추가하거나 할 때 기존 코드베이스에 녹여내기 쉬워지므로 기능을 추가하거나 확장하는데에 드는 시간이 많이 줄어든다.

모듈화가 잘 되어있으면 전체 코드베이스 중 작은 일부만 이해하면 된다. 코드가 명확하면 버그를 만들 가능성도 줄고, 디버깅도 쉽다.

### 언제 리팩터링 해야할까?

저자의 경우 3의 법칙을 따른다고 한다

3의 법칙은 다음과 같다.

1. 처음에는 그냥 한다.
2. 비슷한 일을 두 번째로 하게되면 일단 계속 진행한다.
3. 비슷한 일을 세 번째 하게되면 리팩터링한다.

// 향후 정리예정
