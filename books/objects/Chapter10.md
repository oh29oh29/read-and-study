# 10. 상속과 코드 재사용

재사용 관점에서 상속이란 클래스 안에 정의된 인스턴스 변수와 메서드를 자동으로 새로운 클래스에 추가하는 구현 기법이다.

### 상속과 중복 코드

#### DRY 원칙

중복 코드는 변경을 방해한다.

중복 코드를 판단하는 기준은 변경이다.  
요구사항이 변경됐을 때 두 코드를 함께 수정해야 한다면 이 코드는 중복이다.  
모양이 유사하다는 것은 단지 중복의 징후일 뿐 중복 여부를 결정하는 기준은 코드가 변경에 반응하는 방식이다.

DRY는 Don't Repeat Yourself 의 약자로 동일한 지식을 중복하지 말라는 것이다.  
DRY 원칙은 한 번, 단 한번(Once and Only Once) 원칙 또는 단일 지점 제어(Single-Point Control) 원칙이라고도 한다.

핵심은 코드 안에 중복이 존재해서는 안 된다는 것이다.

#### 상속을 이용해서 중복 코드 제거하기

상속은 이미 존재하는 클래스와 유사한 클래스가 필요하다면 코드를 복사하지 말고 상속을 이용해 코드를 재사용하라는 것이다.

하지만 상속을 이용해 코드를 재사용하기 위해서는 부모 클래스의 개발자가 세웠던 가정이나 추론 과정을 정확하게 이해해야 한다.  
이것은 자식 클래스의 작성자가 부모 클래스의 구현 방법에 대한 정확한 지식을 가져야 한다는 것을 의미한다.

따라서 상속은 결합도를 높인다.  
그리고 상속이 초래하는 부모 클래스와 자식 클래스 사이에 강한 결합이 코드를 수정하기 어렵게 만든다.

### 취약한 기반 클래스 문제

부모 클래스의 변경에 의해 자식 클래스가 영향을 받는 현상을 취약한 기반 클래스 문제(Fragile Base Class Problem, Brittle Base Class Problem)라고 한다.  
이 문제는 상속을 사용한다면 피할 수 없는 객체지향 프로그래밍의 근본적인 취약성이다.

취약한 기반 클래스 문제는 캡슐화를 약화시키고 결합도를 높인다.  
상속은 자식 클래스가 부모 클래스의 구현 세부사항에 의존하도록 만들기 때문에 캡슐화를 약화시킨다.

#### 불필요한 인터페이스 상속 문제

`Stack`과 `Properties`의 예는 퍼블릭 인터페이스에 대한 고려 없이 단순히 코드 재사용을 위해 상속을 이용하는 것이 얼마나 위험한지를 잘 보여준다.  
단순히 코드를 재사용하기 위해 불필요한 오퍼레이션이 인터페이스에 스며들도록 방치해서는 안 된다.

#### 메서드 오버라이딩의 오작용 문제

자식 클래스가 부모 클래스의 메서드를 오버라이딩할 경우 부모 클래스가 자신의 메서드를 사용하는 방법에 자식 클래스가 결합될 수 있다.

클래스가 상속되기를 원한다면 상속을 위해 클래스를 설계하고 문서화해야 한다.  

#### 부모 클래스와 자식 클래스의 동시 수정 문제

결합도란 다른 대상에 대해 알고 있는 지식의 양이다.  
상속은 기본적으로 부모 클래스의 구현을 재사용한다는 기본 전제를 따르기 때문에 자식 클래스가 부모 클래스의 내부에 대해 속속들이 알도록 강요한다.  
따라서 코드 재사용을 위한 상속은 부모 클래스와 자식 클래스를 강하게 결합시키기 때문에 함께 수정해야 하는 상황 역시 빈번하게 발생할 수밖에 없는 것이다.

### Phone 다시 살펴보기

#### 추상화에 의존하자

코드 재사용을 위한 상속의 문제를 해결하는 가장 일반적인 방법은 추상화에 의존하도록 만드는 것이다.  
부모 클래스와 자식 클래스 모두 추상화에 의존하도록 수정해야 한다.

#### 차이를 메서드로 추출하라

중복 코드 안에서 차이점을 별도의 메서드로 추출하라.  
흔히 말하는 "변하는 것으로부터 변하지 않는 것을 분리하라" 또는 "변하는 부분을 찾고 이를 캡슐화하라"라는 조언을 메서드 수준에서 적용한 것이다.

#### 중복 코드를 부모 클래스로 올려라

부모 클래스를 추가하자.  
목표는 모든 클래스들이 추상화에 의존하도록 만드는 것이기 때문에 이 클래스는 추상 클래스로 구현하는 것이 적합하다.

#### 추상화가 핵심이다

공통 코드를 이동시킨 후에 각 클래스는 서로 다른 변경의 이유를 갖게 되었다.  
단일 책임 원칙을 준수하게 되었고 때문에 응집도가 높아졌다.

부모 클래스 역시 자신의 내부에 구현된 추상 메서드를 호출하기 때문에 추상화에 의존한다고 말할 수 있다.  
의존성 역전 원칙도 준수한다.

새로운 클래스를 추가하기도 쉽다.  
확장에는 열려 있고 수정에는 닫혀 있기 때문에 개방-폐쇄 원칙 역시 준수한다.

이런 모든 장점은 클래스들이 추상화에 의존하기 때문에 얻어지는 장점이다.

### 차이에 의한 프로그래밍

기존 코드와 다른 부분만을 추가함으로써 애플리케이션의 기능을 확장하는 방법을 차이에 의한 프로그래밍(programming by difference)이라고 부른다.  
상속을 이용하면 이미 존재하는 클래스의 코드를 쉽게 재사용할 수 있기 때문에 애플리케이션의 점진적인 정의(incremental definition)가 가능해진다.

상속이 코드 재사용이라는 측면에서 매우 강력한 도구인 것은 사실이지만 오용과 남용은 애플리케이션을 이해하고 확장하기 어렵게 만든다.  
정말로 필요한 경우에만 상속을 사용해야 한다.

상속은 코드 재사용과 관련된 대부분의 경우에 우아한 해결 방법은 아니다.  
상속의 단점을 피하면서도 코드를 재사용할 수 있는 더 좋은 방법인 합성이 있다.