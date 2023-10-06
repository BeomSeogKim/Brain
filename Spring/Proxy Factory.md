자바에서 프록시를 생성하는 방법은 다음과 같다.

- 인터페이스가 있는 경우 : JDK Dynamic Proxy를 사용해 프록시 생성
- 인터페이스가 없는 경우 : CGLIB를 사용해 프록시 생성 

Spring에서는 두가지 경우에 대해 유연하게 프록시를 생성할 수 있도록 ProxyFactory를 제공한다. 

![[Pasted image 20231006193636.png]]

Proxy Factory가 프록시 생성 기술을 선택하는 기준은 다음과 같다. 

- 인터페이스가 있는 경우 : JDK Dynamic Proxy 선택
- 인터페이스가 없는 경우 : CGLIB 선택
- 인터페이스가 있는 경우 + proxyTargetClass(true) : CGLIB 선택

***Spring Boot에서는 기본적으로 proxyTargetClass 옵션이 true이다. 따라서 인터페이스가 있어도 CGLIB 방식을 통해 프록시를 생성한다.***

#### Advice

프록시를 생성하는 기술마다 구현하는 구현체가 다르다. 
- JDK Dynamic Proxy -> InvocationHandler
- CGLIB -> Method Interceptor

스프링에서는 부가기능을 제공하기 위해 Advice라는 개념을 도입했다.

![[Pasted image 20231006194617.png]]

프록시를 구현한 기술에 종속되지 않고 Ad