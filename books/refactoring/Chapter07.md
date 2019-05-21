# 07. 객체 간의 기능 이동

### 메소드 이동 (Move Method)

> 메소드가 자신이 속한 클래스보다 다른 클래스의 기능을 더 많이 이용할 땐 제일 많이 이용하는 클래스 안에서 비슷한 내용의 새 메소드를 작성한다.
> 기존 메소드는 간단한 대리 메소드로 전환하든지 삭제한다.

##### 동기

* 클래스에 기능이 너무 많거나 클래스가 다른 클래스와 과하게 연동되어 의존성이 지나칠 때는 메소드를 옮기는 것이 좋다.
* 옮길 만한 메소드가 빌갼되면 그 메소드를 호출하는 메소드, 그 메소드가 호출하는 메소드, 상속 계층에서 그 메소드를 재정의하는 메소드를 살펴본다. 옮기려는 메소드가 더 많이 참조한다고 생각되는 메소드가 들어 있는 객체를 기준으로 해서 계속 진행할지를 판단한다.
* 메소드를 옮길지 확신이 서지 않을 때는 다른 메소드를 살펴본다.
* 판단하기 쉽지 않다는 것은 문제가 있다는 의미이기도 하다.

##### 방법

1. 원본 클래스에 정의되어 있는 원본 메소드에 사용된 모든 기능을 확인한다. 그 기능들도 전부 옮겨야 할지 판단한다. 옮길 메소드에만 사용되는 기능도 함께 옮겨야 한다.
2. 원본 클래스의 하위클래스와 상위클래스에서 그 메소드에 대한 다른 선언이 있는지 확인한다. 다른 선언이 있다면 대상 클래스에도 재정의를 넣을 수 있을 때만 옮길 수 있을지도 모른다.
3. 그 메소드를 대상 클래스 안에 선언한다.
4. 원본 메소드의 코드를 대상 메소드에 복사한 후, 대상 클래스 안에서 잘 돌아가게끔 대상 메소드를 약간 수정한다. 대상 메소드가 원본 메소드를 사용한다면 대상 메소드 안에서 원본 객체를 참조할 방법을 정해야 한다. 대상 클래스에 원본 객체를 참조하는 기능이 없다면 원본 객체 참조를 대상 메소드에 매개변수로 전달한다.
5. 대상 클래스를 컴파일한다.
6. 원본 객체에서 대상 객체를 잠조할 방법을 정한다. 대상 클래스를 참조하는 속성이나 메소드가 이미 존재할 수도 있지만, 혹시 없다면 대상 클래스를 참조하는 메소드를 쉽게 작성할 수 있는지 살펴봐서, 쉽지 않다면 원본 클래스 안에 대상 클래스를 저장할 수 있는 새 속성을 선언해야 한다.
7. 원본 메소드를 위임 메소드로 전환한다.
8. 컴파일과 테스트를 실시한다.
9. 원본 메소드를 삭제하든지, 위임 메소드로 사용하게 내버려둔다.
10. 원본 메소드를 삭제할 때는 기존의 참조를 전부 대상 메소드 참조로 수정한다.
11. 컴파일과 테스트를 실시한다.

<br>

### 필드 이동 (Move Field)

> 어떤 필드가 자신이 속한 클래스보다 다른 클래스에서 더 많이 사용될 때는 대상 클래스 안에 새 필드를 선언하고 그 필드 참조 부분을 전부 새 필드 참조로 수정한다.

##### 동기

* 한 클래스에서 다른 클래스로 상태와 기능을 옮기는 것은 리팩토링의 기본이다.
* 어떤 필드가 자신이 속한 클래스보다 다른 클래스에 있는 메소드를 더 많이 참조해서 정보를 이용한다면 그 필드를 옮기는 것을 고민해야 한다.
* 인터페이스에 따라 메소드를 옮기는 방법을 사용할 수 있지만, 메소드의 현재 위치가 적절하다면 필드를 옮긴다.
* 클래스 추출을 실시하는 중에도 필드를 옮기는 기법이 수반된다. 이럴 땐 필드가 우선이고 메소드는 다음이다.

##### 방법

1. 필드가 public이면 필드 캡슐화 기법을 실시한다. 필드에 자주 접근하는 메소드를 옮겨야 하거나, 그 필드에 많은 메소드가 접근할 때는 필드 자체 캡슐화를 실시한다.
2. 컴파일과 테스트를 실시한다.
3. 대상 클래스 안에 읽기/쓰기 메소드와 함께 필드를 작성한다.
4. 대상 클래스를 컴파일한다.
5. 원본 객체에서 대상 객체를 참조할 방법을 정한다.
6. 원본 클래스에서 필드를 삭제한다.
7. 원본 필드를 참조하는 모든 부분을 대상 클래스에 있는 적절한 메소드를 참조하게 수정한다.
8. 컴파일과 테스트를 실시한다.

<br>

### 클래스 추출 (Extract Class)

> 두 클래스가 처리해야 할 기능이 하나의 클래스에 들어 있을 땐 새 클래스를 만들고 기존 클래스의 관련 필드와 메소드를 새 클래스로 옮긴다. 

##### 동기

* 시간이 지날수록 클래스는 방대해지며 이해하기 힘들어진다. 클래스의 어느 부분을 분리할지 고민해서 떼어내야 한다.
* 데이터의 일부분과 메소드의 일부분이 한 덩어리이거나, 주로 함께 변화하거나 서로 유난히 의존적인 데이터의 일부분도 클래스로 떼어내기 좋다.
* 판단하는 좋은 방법은 데이터나 메소드를 하나 제거하면 어떻게 될지, 다른 필드와 메소드를 추가하는 건 합리적이지 않은지 고민하는 것이다.

##### 방법

1. 클래스의 기능 분리 방법을 정한다.
2. 분리한 기능을 넣을 새 클래스를 작성한다.
3. 원본 클래스에서 새 클래스로의 링크를 만든다. 양방향 링크를 만들어야 할 수도 있는데, 필요할 때까진 역방향 링크를 만들지 않는다.
4. 옮길 필드마다 필드 이동을 적용한다.
5. 필드를 하나씩 옮길 때마다 컴파일과 테스트를 실시한다.
6. 메소드 이동을 실시해서 원본 클래스의 메소드를 새 클래스로 옮긴다. 피호출 메소드부터 시작해서 호출 메소드에 적용한다.
7. 메소드 이동을 실시할 때마다 테스트를 실시한다.
8. 각 클래스를 다시 검사해서 인터페이스를 줄인다. 양방향 링크가 있다면 그것을 단방향으로 바꿀 수 있는지 알아본다.
9. 여러 곳에서 클래스에 접근할 수 있게 할지 결정한다. 여러 곳에서 접근할 수 있게 할 경우, 새 클래스를 참조 객체나 변경불가 값 객체로서 공개할지 여부를 결정한다.

<br>

### 클래스 내용 직접 삽입 (Inline Class)

> 클래스에 기능이 너무 적을 땐 그 클래스의 모든 기능을 다른 클래스로 합쳐 넣고 원래의 클래스는 삭제한다.

##### 동기

* 클래스 추출과 반대다.
* 클래스가 더 이상 제 역할을 수행하지 못하여 존재할 이유가 없을 때 실시한다.
* 주로 클래스의 기능 대부분을 다른 곳으로 옮기는 리팩토링을 실시해서 남은 기능이 거의 없어졌을 때 나타난다.
* 작아진 클래스를 가장 많이 사용하는 다른 클래스를 하나 고른 후, 그 클래스에 합친다.

##### 방법

1. 원본 클래스의 public 프로토콜 메소드를 합칠 클래스에 선언하고, 이 메소드를 전부 원본 클래스에 위임한다.
2. 원본 클래스의 모든 참조를 합칠 클래스 참조로 수정한다.
3. 컴파일과 테스트를 실시한다.
4. 메소드 이동과 필드 이동을 실시해서 원본 클래스의 모든 기능을 합칠 클래스로 옮긴다.
5. 원본 클래스를 삭제한다.

<br>

### 대리 객체 은폐 (Hide Delegate)

> 클라이언트가 객체의 대리 클래스를 호출할 땐 대리 클래스를 감추는 메소드를 서버에 작성한다.

##### 동기

* 클라이언트가 서버 객체의 필드 중 하나에 정의된 메소드를 호출할 때 그 클라이언트는 이 대리 객체에 관해 알아야 한다. 대리 객체가 변경될 때 클라이언트도 변경해야 할 가능성이 있기 때문이다. 이러한 의존성을 없애려면, 대리 객체를 감추는 간단한 위임 메소드를 서버에 두면 된다. 변경은 서버에만 이뤄지고 클라이언트에는 영향을 주지 않는다.
* 서버의 일부 클라이언트나 모든 클라이언트에 대리 객체 은폐를 실시하는 것이 좋을 때도 있다. 모든 클라이언트를 대상으로 대리 객체를 감출 경우에는 서버의 인터페이스에서 대리 객체에 대한 모든 부분을 삭제해도 된다.

##### 방법

1. 대리 객체에 들어 있는 각 메소드를 대상으로 서버에 간단한 위임 메소드를 작성한다.
2. 클라이언트를 수정해서 서버를 호출하게 만든다. 클라이언트 클래스가 서버 클래스와 같은 패키지에 들어 있지 않다면 대리 메소드의 접근을 같은 패키지에 있는 클래스만 접근할 수 있게 수정하는 것을 고려한다.
3. 각 메소드를 수정할 때마다 컴파일과 테스트를 실시한다.
4. 대리 객체를 읽고 써야 할 클라이언트가 하나도 남지 않게 되면, 서버에서 대리 객체가 사용하는 읽기/쓰기 메소드를 삭제한다.
5. 컴파일과 테스트를 실시한다.

<br>

### 과잉 중개 메소드 제거 (Remove Middle Man)

> 클래스에 자잘한 위임이 너무 많을 땐 대리 객체를 클라이언트가 직접 호출하게 한다.

##### 동기

* 대리 객체 은폐를 실시하면 단점도 생긴다. 클라이언트가 대리 객체의 새 기능을 사용해야 할 때마다 서버에 간단한 위임 메소드를 추가해야 한다는 점이다.
* 서버 클래스는 중개자에 불과하므로, 클라이언트가 대리 객체를 직접 호출하게 해야 한다.

##### 방법

1. 대리 객체에 대한 접근 메소드를 작성한다.
2. 대리 메소드를 클라이언트가 사용할 때마다 서버에서 메소드를 제거하고 클라이언트에서의 호출을 대리 객체에서의 메소드 호출로 교체한다.
3. 메소드를 수정할 때마다 테스트를 실시한다.

<br>

### 외부 클래스에 메소드 추가 (Introduce Foreign Method)

> 사용 중인 서버 클래스에 메소드를 추가해야 하는데 그 클래스를 수정할 수 없을 땐 클라이언트 클래스 안에 서버 클래스의 인스턴스를 첫 번째 인자로 받는 메소드를 작성한다.

##### 동기

* 원본 클래스가 수정 가능하다면 추가해야 하는 기능 메소드를 추가하면 되지만, 수정할 수 없는 원본 클래스라면 그 메소드를 클라이언트 클래스 안에 작성해야 한다.
* 이 리팩토링 기법을 실시할 때 새로 만들 메소드를 외래 메소드로 만들면 그 메소드가 원래는 원본 메소드인 서버 메소드에 있어야 할 메소드임을 분명히 나타낼 수 있다.
* 서버 클래스에 수많은 외래 메소드를 작성해야 하거나 하나의 외래 메소드를 여러 클래스가 사용해야 할 때는 이 기법 대신 국소적 상속확장 클래스 사용 기법을 실시한다.

##### 방법

1. 필요한 기능의 메소드를 클라이언트 클래스 안에 작성한다. 그 메소드는 클라이언트 클래스의 어느 기능에도 접근해선 안 된다. 그 메소드에 값이 필요할 땐 매개변수로 전달해야 한다.
2. 서버 클래스의 인스턴스를 첫 번째 매개변수로 만든다.
3. 그 메소드에 '서버 클래스에 있을 외래 메소드' 같은 주석을 단다. 나중에 그 외래 메소드를 옮길 일이 생겼을 때 문자열 검색 기능으로 외래 메소드를 쉽게 찾을 수 있다.

<br>

### 국소적 상속확장 클래스 사용 (Introduce Local Extension)

> 사용 중인 서버 클래스에 여러 개의 메소드를 추가해야 하는데 클래스를 수정할 수 없을 땐 새 클래스를 작성하고 그 안에 필요한 여러 개의 메소드를 작성한다.
> 이 상속확장 클래스를 원본 클래스의 하위클래스나 래퍼 클래스로 만든다.

##### 동기

* 원본 클래스가 불가능할 때, 추가해야 하는 메소드가 적다면 외래 클래스에 메소드 추가 기법을 실시하면 되지만 추가해야 하는 메소드가 많다면 적당한 곳에 모아두고 하위클래스화와 래퍼화를 실시한다.
* 이렇게 만든 하위클래스와 래퍼 클래스를 국소적 상속확장 클래스라고 부른다.
* 국소적 상속확장 클래스는 별도의 클래스지만 상속확장하는 클래스의 하위 타입이다. 원본 클래스의 모든 기능도 사용 가능하면서 추가 기능도 사용할 수 있다.
* 국소적 상속확장 클래스를 사용하면 메소드와 데이터가 체계적인 단위로 묶여야 한다는 원칙이 저절로 지켜진다.

##### 방법

1. 상속확장 클래스를 작성한 후 원본 클래스의 하위클래스나 래퍼 클래스로 만든다.
2. 상속확장 클래스에 변환 생성자 메소드를 작성한다. 생성자는 원본 클래스를 인자로 받는다. 하위클래스의 경우 적절한 상위클래스 생성자를 호출하며, 래퍼 클래스의 경우 대리 필드에 그 인자를 할당한다.
3. 상속확장 클래스에 새 기능을 추가한다.
4. 필요한 위치마다 원본 클래스를 상속확장 클래스로 수정한다.
5. 이 클래스용으로 정의된 외래 메소드를 전부 상속확장 클래스로 옮기자.