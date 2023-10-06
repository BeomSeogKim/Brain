자바에서 프록시를 생성하는 방법은 다음과 같다.
- 인터페이스가 있는 경우 : JDK Dynamic Proxy를 사용해 프록시 생성
- 인터페이스가 없는 경우 : CGLIB를 사용해 프록시 생성 

Spring에서는 두가지 경우에 대해 유연하게 프록시를 생성할 수 있도록 ProxyFactory를 제공한다. 

![[Pasted image 20231006193636.png]]
