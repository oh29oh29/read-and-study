# 09. LSP: 리스코프 치환 원칙

### 상속을 사용하도록 가이드하기

calcFee()라는 메서드를 가진 License 클래스가 있다.  
Billing 애클리케이션에서 calcFee() 메서드를 호출한다.  
License에는 PersonalLicense와 BusinessLicense라는 두 가지 '하위 타입'이 존재한다.  

이 설계는 LSP를 준수하는데, Billing 애플리케이션의 행위가 License 하위 타입 중 무엇을 사용하는지에 전혀 의존하지 않기 때문이다.  
하위 타입은 모두 License 타입을 치환할 수 있다.

### 정사각형/직사각형 문제

LSP를 위반하는 전형적인 문제로는 정사각형/직사각형(square/rectangle) 문제가 있다.  

Rectangle(setH(), setW()) 클래스가 있고, Square(setSide())라는 하위 타입이 존재한다.
User가 Rectangle만 보고 사용하는 입장이라면 혼동이 생길 수 있다.

Rectangle의 높이와 너비는 서로 독립적으로 변경될 수 있지만,  
Square의 높이와 너비는 반드시 함께 변경되기 때문에  
Square는 Rectangle의 하위 타입으로는 적합하지 않다.

### LSP와 아키텍처

LSP는 상속을 사용하도록 가이드하는 방법 정도로 간주되었다.  
하지만 시간이 지나면서 LSP는 인터페이스와 구현체에도 적용되는 더 광범위한 소프트웨어 설계 원칙으로 변모해 왔다.



