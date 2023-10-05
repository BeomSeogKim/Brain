동적 프록시 기술은 Proxy 객체를 동적으로 생성할 수 있는 기능을 지닌다. 
Spring에서 주로 사용되는 동적 프록시 기술은 `JDK Dynamic Proxy`, `CGLIB` 이다.

### JDK Dynamic Proxy

JDK 동적 프록시는 인터페이스를 기반으로  프록시를 동적으로 생성한다. 그렇기에 인터페이스가 필수적이다. 

#### Handler 구현
```java
@Slf4j  
public class TimeInvocationHandler implements InvocationHandler {  
  
    @Override  
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {  
        return null; 
    }}
```

프록시에 적용하고자 하는 로직은 InvocationHandler를 구현해 적용하면된다. 
invoke 메서드 안에 구현하고자 하는 로직들을 적용하면된다.

#### Proxy 생성

```java
AInterface target = new AImpl();  
  
TimeInvocationHandler handler = new TimeInvocationHandler(target);  
AInterface proxy =  
        (AInterface) Proxy.newProxyInstance(AInterface.class.getClassLoader(), new Class[]{AInterface.class}, handler);
```

`Proxy.newProxyInstance`를 사용해 프록시를 생성할 수 있다. 
필요한 파라미터는 순차적으로 다음과 같다. 
1. ClassLoader (Interfc)
2. Class