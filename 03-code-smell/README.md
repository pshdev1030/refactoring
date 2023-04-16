리팩터링을 언제 시작하고 언제 그만할 지를 판단하는 일은 리팩터링의 작동 원리를 아는 것 못지 않게 중요하다.

3장에서는 리팩터링의 몇 가지 징조에 대해서 서술하였다.

## 3-1 기이한 이름

코드를 명료하게 표현하는데에 가장 중요한 요소 중 하나는 바로 '이름'이다.
이름만 보고도 무슨 일을 하고 어떻게 사용해야 하는지 명확히 알 수 있도록 이름을 지어야 한다.
만약 마땅한 이름이 떠오르지 않는다면 설계에 더 근본적인 문제가 숨어있을 가능성이 높다.
혼란스러운 이름을 잘 정리하다 보면 코드가 훨씬 간결해질 때가 많다.

## 3-2 중복 코드

똑같은 코드 구조가 여러 곳에서 반복된다면 하나로 통합하여 더 나은 프로그램을 만들 수 있다.
코드가 중복되면 각각을 볼 때마다 서로 차이점은 없는지 사려봐야하는 부담이 생기고, 하나를 수정할 때 다른 코드들도 비슷하게 수정해야한다.

### 3-3 긴 함수

오랜 기간 동안 잘 활용되는 프로그램들은 하나같이 짧은 함수로 구성됐다.
코드를 끝없이 위임하는 방식으로 작성되어있기 때문이다.

간접 호출의 효과, 즉 코드를 이해하고, 공유하고, 선택하기 쉬워지는 장점은 함수를 짧게 구성할 때 나오는 것이다.

3-1의 기이한 이름과도 연관이 있다. 짧은 함수로 구성된 코드를 이해하기 쉽게 만드는 방법은 함수 이름을 잘 짓는 것이다.
함수의 역할이 이름에 더 잘 드러나게 하기 위해선 적극적으로 함수를 쪼개야한다.

주석을 달만한 부분을 함수로 쪼개어 함수 본문엔 주석으로 설명하려는 코드가 담기고 이름에는 동작 방식이 아닌 의도가 드러나게 짓는다.

핵심은 함수의 목적과 구현코드의 괴리가 얼마나 큰가이다. 즉 코드가 무엇을 하는지 설명하기 어려울 수록 함수로 만드는게 유리하다.

즉 목적이 명료한 한 가지 작업을 한 가지 함수로 분리하여 이름과 코드로 목적과 구현방식을 설명할 수 있도록 해야한다.

### 3-4 긴 매개변수 목록

매개변수 목록이 길어지면 그 자체로 이해하기 어려울 때가 많다.

### 3-5 전역 데이터

전역 데이터를 주의해야한다.

전역데이터는 코드베이스 어디에서든 건드릴 수 있고, 값을 누가 바꿨는지 찾아낼 메커니즘이 없다는게 문제다.

즉 버그는 발생하는데 원인이 되는 코드를 찾아내기가 굉장히 어렵다.

이를 방지하기 위해선 다른 코드를 오염시킬 가능성이 있는 데이터를 발견할 때 마다 캡슐화 하는 등 많은 방법이 있다.

즉 접근범위를 줄이는 것이다.

### 3-6 가변 데이터

데이터를 변경했을 때 예상치 못한 결과나 골치아픈 버그로 이어지는 경우가 종종 있다.

즉 무분별한 데이터 수정으로 인해 추적하기 어려운 버그가 발생하는 경우가 있다.

함수형 프로그래밍에선 불변성을 지키기 위해 데이터는 변하지 않고, 데이터를 변경하려면 변경하려는 값에 해당하는 복사본을 만들어서 반환한다는 개념을 기본으로 삼고있다.

이 또한 정해놓은 함수를 거쳐야 값을 수정할 수 있도록 캡슐화 하면 추적이 쉬워진다.

혹은 하나의 변수에 용도가 다른 여러값을 저장하며 갱신하지 않고 독립변수를 사용하는 방벙도 있다.

### 3-7 뒤엉킨 변경

소프트웨어에서 코드를 수정할 때는 고쳐야 할 딱 한 군데를 찾아서 그 부분만 수정할 수 있기를 바란다.

이렇게 할 수 없다면, 그 이유는 단일 책임 원칙을 제대로 지키지 않아서이다.

즉 하나의 모듈이 서로 다른 이유들로 인해 여러가지 방식으로 변경되는 일이 많을 때 발생한다.

이런 일이 발생하지 않도록 단계를 분리하고 모듈단위로 잘 쪼개야한다.

### 3-8 산탄총 수술

3-7 뒤엉킨 변경과 비슷하면서 정 반대이다.

변경할 부분이 코드 전반에 퍼져있어서 코드를 변경할 떄마다 자잘하게 수정해야 하는 클래스가 많은 현상이다.

변경되는 대상들을 모두 한 모듈에 묶어두면 좋다.

즉 단계나 맥락별로 적절하게 모듈단위로 분리하면서 함께 변경되는 대상들 끼리는 한 모듈로 묶어서 관리해야한다.

### 3-9 기능 편애

프로그램을 모듈화할 때는 코드를 여러 영역으로 나눈 뒤, 영역 안에서 이뤄지는 상호작용은 최대한 늘리고 영역 사이에서 이뤄지는 상호작용은 최소로 줄이는 데에 주력해야한다.

기능 편애는 자기가 속한 모듈의 함수나 데이터보다 다른 모듈의 함수나 데이터와 상호작용 할 일이 더 많을 때 풍기는 냄새다.

예를들어 실행과정에서 외부 객체의 게터 메서드 대여섯 개를 호출하도록 작성된 함수가 있다면. 이는 기능편애이다.

함수가 데이터와 가까이 있고 싶어 한다는 의중이 뚜렷이 드러나므로 소원대로 데이터 근처로 옮겨주면 된다.

떄로는 함수의 일부에서만 기능을 편애할 수 있다. 이럴 때는 그 부분만 독립함수로 빼낸다음 원하는 모듈로 보낼 수 있다.

종종 어디로 옮길지가 명확하게 드러나지 않는 경우가 있다. 해당 경우에는 함수를 여러 조각으로 나눈 후 각각을 적합한 모듈로 옮겨서 해결할 수 있다.

즉 가장 기본이 되는 것은 함께 변경할 대상을 한데 모으는 것이다.

### 3-10 데이터 뭉치

데이터 항목들은 서로 연관이 있는 경우가 많다.

즉 데이터 항목 서러개가 여러곳에서 항상 함께 뭉쳐 다니는 모습을 흔히 목격할 수 있다.

이렇게 몰려다니는 데이터 뭉치는 보금자리를 따로 마련해주어야한다.

클래스로 추출하고, 매개변수 객체를 만들거나 객체를 통째로 넘기도록 하여 매개변수 수를 줄여 호출 코드또한 간결하게 만들 수 있다.

이런 데이터 뭉치를 판별하는 방법은 데이터중 하나를 제거했을 경우 나머지 데이터만으로는 의미가 없어질 경우 객체로 환생하길 갈망하는 데이터 뭉치라는 것이다.

### 3-11 기본형 집착

대부분의 프로그래밍 언어는 다양한 primitive type을 제공한다.

이러한 private type을 다룰 때는 주어진 문제에 맞는 기초타입( 화폐, 좌표, 구간 )등을 직접 정의해야한다.

### 3-12 반복되는 switch문

똑같은 조건부 로직(switch/case 문이나 길게 나열된 if/else문) 이 여러 곳에서 반복해 등장하는 코드에 집중해보자

중복된 switch문이 문제가 되는 이유는 조건절을 하나 추가할 때 마다 다른 switch문들도 모두 찾아서 수정해야하기 때문이다.

다형성을 지킬 수 있도록 작성하는 것이 좋다.

### 3-13 반복문

반복문은 파이프라인으로 바꾸어 반복문을 제거할 수 있다.

### 3-14 성의 없는 요소

필요없는 프로그래밍 요소(함수, 클래스, ...etc)등은 제거하는 것이 좋다.

### 3-15 추측성 일반화

나중에 필요할거야 라는 생각으로 작성한 모든 종류의 후킹 포인트와 특이 케이스 처리 로직을 작성해둔 코드는 이해하거나 관리하기 어려워진다.

실제로 사용하게 되면 다행이지만, 그렇지 않는다면 쓸데없는 시간 낭비일 뿐이다. 당장 걸리적거리는 코드는 제거하자.

### 3-16 임시 필드

간혹 특정 상황에서만 값이 설정되는 필드를 가진 클래스도 있다.
하지만 객체를 가져오는 입장에선 당연히 모든 필드가 채워져 있으리라 기대하는 게 보통이다.
이렇게 임시 필드를 갖도록 작성하면 코드를 이해하기 어렵다.

임시 필드들과 관련된 코드는 새 클래스로 추출하는 것이 일반적이다.
혹은 특이케이스를 추가하여 필드들이 유효하지 않을 때를 위한 대안 클래스를 만들어 제거할 수 있다.

### 3-17 메시지 체인

메시지 체인은 클라이언트가 한 객체를 통해 다른 객체를 얻고, 그 객체에서 다른 객체를 요청하는 식으로, 다른 객체를 요청하는 작업이 연쇄적으로 이어지는 코드를 말한다.

예를들어 연속적으로 게터가 꼬리를 물고 이어지거나 임시변수가 줄줄이 나열되는 코드이다.

보통 위임을 숨겨서 해결할 수 있다.

즉 연속적인 게터의 위임을 위로 끌어서 위임을 숨기는 것이다.

### 3-18 중개자

객체의 대표적인 기능 중 캡슐화가 있다.

캡슐화 하는 과정에서는 위임이 자주 활용된다.

하지만 위임이 너무 지나칠 경우 중개자를 제거하여 실제로 일을 하는 객체와 직접 소통하게 해야한다.

### 3-19 내부자 거래

모듈 사이의 데이터 거래가 많으면 결합도가 높아진다.

이를 피하기 위해 모듈간 데이터 거래를 줄이고 모두 투명하게 처리해야한다.

여러 모듈이 같은 관심사를 공유한다면 공통 부분을 정식으로 처리하는 제 3의 모듈을 만들거나 위임을 숨겨 다른 모듈이 중간자 역할을 하도록 만들 수 있다.

### 3-20 거대한 클래스

한 클래스가 상당히 많은 일을 하려다 보면 필드 수가 상당히 늘어난다.

이럴 경우 필드들 일부를 따로 묶어 여러개의 클래스로 분리할 수 있다.

혹은 클래스 내에서 자체적인 중복을 제거하고 메소드로 뽑아내어 코드량을 줄일 수도 있다.

클라이언트에서 거대 클래스를 이용하며 특정 기능만 사용한다면 그 각각의 기능 그룹이 개별 클래스로 추출될 후보이다.

### 3-21 서로 다른 인터페이스의 대안 클래스들

클래스를 다른 클래스로 교체해야 할 경우가 있을 수 있다.
이를 대비하여 클래스들의 메서드 시그니처를 일치시키거나 중복된 부분을 슈퍼클래스로 추출하여 해결할 수 있다.

### 3-22 데이터 클래스

데이터 클래스는 게터,세터로만 구성된 클래스이다.

변경하면 안되는 필드는 세터를 제거해서 접근을 원천봉쇄하고 public 필드는 캡슐화해야한다.

### 3-23 상속 포기

서브클래스는 부모클래스부터 상속은 모든 메서드와 데이터를 물려받는다.

하지만 관심있는 몇 가지만 상속받으려 하거나 필요 없는 부분이 있는경우도 있을 수 있다.

예전에는 계층구조 설계가 잘못됐다고 보고 같은 계층에 서브클래스를 추가해서 메서드와 필드를 이 서브클래스로 옮겨 해결하곤 했다.

하지만 항상 이렇게 해야하는 것은 아니다.

상속 포기는 주로 서브클래스가 부모의 동작은 필요로 하지만 인터페이스는 따르고 싶지 않을 때 이런 상황이 많이 발생한다.

이럴 경우 서브 상속 메커니즘에서 벗어나는 것이 유리하다.

### 3-24 주석

주석은 좋지만 주석을 너무 장황하게 달았다면 코드를 잘못 작성했을 가능성이 크다.

함수 이름으로 기능을 설명하고 본문으로 함수가 하는 일을 설명할 수 있도록 작성해보자.

## 느낀점

리팩터링이 필요한 몇몇 징조에 대해서 살펴보았는데 각 항목들에서 느낀 점은 다음과 같다.

1. 함수를 적절한 모듈단위로 분리하자.

함수를 적절한 모듈단위로 분리하면, 하나의 클래스나 함수에서 너무 많은 기능을 하지 않도록 적절히 역할을 분리할 수 있다.

역할을 분리함으로서 얻는 이점은 하나의 함수가 어떤 역할을 하는지 명확해지며, 이는 함수의 이름과 본문으로 함수의 역할을 충분히 설명할 수 있음에 있다.

2. 접근 범위 제한

접근 범위라는 표현이 맞는 표현인지는 모르겠지만, 필요하다면 상속과 서브클래스를 활용해서 실제 필요한 범위에만 접근할 수 있도록 클래스의 접근 범위를 제한해야 한다.

3. 추적이 쉬운 코드

위에서 언급한 전역데이터나 불변성, 뒤엉킨 산탄총등은 추적이 매우 어렵다.

추적이 쉽도록 하기 위해 캡슐화를 활용하거나 2번과 같이 유효범위를 제한할 수 있다.

4. 응집도와 결합도

1번에서 언급한 적절한 모듈 모듈단위라는 것은 결합도는 낮게, 응집도는 높게 모듈단위로 분리하는 것이다.

모듈과 모듈간의 상호 의존도를 줄이고 같은 기능은 모듈 내에 집중하여 결합도를 낮추고 응집도를 높이자.

이는 모듈의 역할이 명확해지고 관리포인트가 줄게 되어 수정에 유리하다.