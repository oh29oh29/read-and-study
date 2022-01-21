# 25. 톱레벨 클래스는 한 파일에 하나만 담으라

소스 파일 하나에 톱레벨 클래스를 여러 개 선언하더라도 자바 컴파일러는 불평하지 않는다.  
하지만 아무런 이득이 없을 뿐더러 심각한 위험을 감수해야 하는 행위다.
한 클래스를 여러 가지로 정의할 수 있으며, 그중 어느 것을 사용할지는 어느 소스 파일을 먼저 컴파일하냐에 따라 달리지기 때문이다.

톱레벨 클래스들을 서로 다른 소스 파일로 분리하면 해결된다.

굳이 여러 톱레벨 큺래스를 한 파일에 담고 싶다면 정적 멤버 클래스를 사용하는 방법을 고민해볼 수 있다.  
다른 클래스에 딸린 부차적인 클래스라면 정적 멤버 클래스로 만드는 쪽이 일반적으로 더 나을 것이다.