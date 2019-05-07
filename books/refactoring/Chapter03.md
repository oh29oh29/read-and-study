# 03. 코드의 구린내

### 중복 코드 (Duplicated Code)

* 똑같은 코드 구조가 두 군데 이상 존재할 때, 그 부분을 하나로 통일하면 프로그램이 개선된다.

1. 두 메소드 안에 같은 코드
    * 메소드 추출 기법을 적용하여 중복 코드를 별도의 메소드로 만들고 호출한다.
2. 한 클래스와 두 하위 클래스에 같은 코드
    * 메소드 추출 기법을 적용하여 중복을 없앤 후, 메소드 상향 기법을 적용한다.
    * 코드가 똑같지 않고 비슷하면, 메소드 추출 기법을 적용해서 같은 부분과 다른 부분을 분리한다. 그 후, 경우에 따라 템플릿 메소드 형성 기법을 적용해야 할 수도 있다.
    * 두 메소드가 알고리즘만 다르고 기능이 같다면 두 알고리즘 중에서 더 간단한 것으로 전환(substitude)한다.
    * 중복 코드가 메소드 가운데에 있다면 주변 메소드 추출 기법을 적용한다.
3. 서로 상관없는 두 클래스 안에 같은 코드
    * 한 클래스 안의 중복 코드를 클래스 추출이나 모듈 추출을 적용해 제 3의 클래스나 모듈로 분리한 후 그것을 다른 클래스에서 호출한다.
    * 중복 코드를 빼서 메소드로 만든 후 그 메소드를 두 클래스 중 하나에 넣고 다른 클래스에서 그 메소드를 호출하거나, 제 3의 클래스에 넣고 두 클래스에서 그 메소드를 호출한다.

<br>

### 장황한 메소드 (Long Method)

* 최적의 상태로 장수하는 프로그램들은 공통적으로 메소드 길이가 짧다.
* 짧은 메소드를 쉽게 이해하는 방법은 기능을 쉽게 알 수 있는 메소드명으로 정하는 것이다.
* 메소드를 줄이려면 대부분 메소드 추출 기법을 적용해야 한다.
* 메소드의 임시변수는 메소드 호출로 전환 기법이나 임시변수를 메소드 체인으로 전환 기법을 적용하면 임시변수가 제거된다.
* 메소드의 매개변수는 매개변수 세트를 객체로 전환 기법과 객체를 통째로 전달 기법을 적용하면 간결해진다.
* 그럼에도 임시변수와 매개변수가 많다면, 메소드를 메소드 객체로 전환 기법을 적용한다.
* 조건문과 루프도 메소드로 빼야 한다. 조건문을 추출하려면 조건문 쪼개기 기법을 사용하고 루프를 컬렉션 클로저 메소드로 전환을 한 후, 그 클로저 메소드 호출과 클로저 자체에 메소드 추출을 적용한다.

<br>

### 방대한 클래스 (Large Class)

* 기능이 많은 클래스에는 보통 많은 인스턴스 변수가 존재한다. 인스턴스 변수가 많으면 중복 코드가 존재할 가능성이 높다.
* 서로 연관된 인스턴스 변수를 클래스 추출을 적용하여 하나로 묶을 수 있다.
* 하위클래스 추출 또는 추출할 클래스가 대리자로 알맞지 않으면 모듈 추출을 적용한다.
* 코드 분량이 방대한 클래스에 대해서도 클래스 추출, 모듈 추출, 하위클래스 추출 중 하나를 적용한다.

<br>

### 과다한 매개변수 (Long Parameter List)

* 매개변수 세트가 길면 서로 일관성이 없어지거나 사용이 불편해지고, 더 많은 데이터가 필요해질 때마다 계속 수정이 필요하다.
* 이미 알고 있는 객체에 요청하여 한 매개변수에 들어 있는 데이터를 가져올 수 있을 때는 매개변수 세트를 메소드로 전환 기법을 적용한다.
* 객체에 있는 데이터 세트를 가져온 후, 데이터 세트를 그 객체 자체로 전환하려면 객체를 통째로 전달 기법을 적용한다.
* 여러 데이터 항목에 논리적 객체가 없다면 매개변수 세트를 객체로 전환 기법을 적용한다.
* 이런 기법들을 적용할 때 예외가 하나 존재한다. 호출되는 객체가 호출 객체에 의존하면 안 될 때다. 이럴 때는 데이터를 개별적으로 뺏 ㅓ매개변수로 전달하는 것이 바람직하다. 나열된 매개변수 세트가 너무 길거나 자주 바뀐다면 종속 구조를 유지하는 것도 방법이다.

<br>

### 수정의 산발 (Divergent Change)

* 한 클래스에 여러 수정이 발생하는 문제이다.
* 수정의 산발은 한 클래스가 다양한 원인 때문에 다양한 방식으로 자주 수정될 때 일어난다.
* 예를 들어, 특정 원인으로 인해 여러 개의 메소드를 수정해야 한다면 그 클래스를 여러 개의 객체로 분리하는 것이 좋다. 그러면 각 객체는 한 종류의 수정에 의해서만 변경된다.
* 특정 원인으로 인해 변하는 모든 부분을 찾은 후 클래스 추출 기법을 적용해서 그 부분들을 합쳐 한 클래스로 빼낸다.


<br>

### 기능의 산재 (Shotgun Surgery)

* 하나의 수정으로 여러 클래스가 바뀌게 되는 문제이다.
* 수정할 때마다 여러 클래스에서 많은 부분을 고쳐야 한다면 이 문제를 의심해야 한다.
* 메소드 이동과 필드 이동을 적용해서 수정할 부분들을 하나의 클래스 안에 넣는다. 기존의 클래스 중에 넣기에 적절하지 않으면 새 클래스에 넣는다.
* 대개 클래스 내용 직접 삽입을 적용해서 별도 클래스에 분산되어 있던 모든 기능을 한 곳으로 가져와도 된다.

<br>

### 잘못된 소속 (Feature Envy)

* 객체의 핵심은 데이터와 그 데이터에 사용되는 프로세스를 하나로 묶는 기술이라는 점이다.
* 어떤 메소드가 자신이 속하지 않은 클래스에 더 많이 접근한다면 잘못된 것이다.
* 소속이 잘못된 메소드는 더 많이 접근하는 클래스로 메소드 이동 기법을 적용해서 옮긴다. 메소드의 일부분만 소속이 잘못된 경우에는 그 부분에 메소드 추출을 적용한 후 메소드 이동을 적용한다.
* 한 메소드가 여러 클래스에 많이 접근할 때는 어느 클래스에 제일 많이 접근하는지 파악해서 그 클래스로 옮긴다. 메소드 추출을 적용해서 그 메소드를 다른 클래스에 들어갈 여러 부분으로 쪼개면 더 좋다.

<br>

### 데이터 뭉치 (Data Clumps)

* 동일한 3~4개의 데이터 항목이 여러 위치에 몰려 있는 경우 객체로 만들어야 한다.
* 데이터 뭉치를 객체로 만들려면 클래스 추출 기법을 적용해야 한다. 그 후, 메소드 시그너처를 대상으로 매개변수 세트를 객체로 전환 기법과 객체를 통째로 전달 기법을 적용한다. 결과적으로 매개변수가 적어져서 메소드 호출 코드가 간결해지는 효과가 있다.