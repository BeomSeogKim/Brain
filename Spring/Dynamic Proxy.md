동적 프록시 기술은 Proxy 객체를 동적으로 생성할 수 있는 기능을 지닌다. 
Spring에서 주로 사용되는 동적 프록시 기술은 `JDK Dynamic Proxy`, `CGLIB` 이다.

### JDK Dynamic Proxy

JDK 동적 프록시는 **인터페이스**를 기반으로  프록시를 동적으로 생성한다. 그렇기에 인터페이스가 필수적이다. 

#### Handler 구현
```java
public class TimeInvocationHandler implements InvocationHandler {  

	private final Object target;

	// ... 
	
    @Override  
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {  
        return method.invoke(target, args); 
    }}
```

프록시에 적용하고자 하는 로직은 InvocationHandler를 구현해 적용하면된다. 
invoke 메서드 안에 구현하고자 하는 로직들을 적용하면된다.

invoke 메서드의 파라미터는 순차적으로 다음과 같다. 
1. 프록시 
2. 호출한 메서드 
3. 메서드 호출시 전달한 인수 

#### Proxy 생성

```java
AInterface target = new AImpl();  
  
TimeInvocationHandler handler = new TimeInvocationHandler(target);  
AInterface proxy =  
        (AInterface) Proxy.newProxyInstance(AInterface.class.getClassLoader(), new Class[]{AInterface.class}, handler);
```

`Proxy.newProxyInstance`를 사용해 프록시를 생성할 수 있다. 
필요한 파라미터는 순차적으로 다음과 같다. 
1. ClassLoader (Interface)
2. Class (Interface)
3. Handler

---

### CGLIB (Code Generator Library)

CGLIB는 바이트코드를 조작해 클래스를 생성하는 기술을 제공한다. 
CGLIB는 인터페이스가 없어도 프록시를 생성할 수 있다. 

#### Handler 구현

```java
public class TimeMethodInterceptor implements MethodInterceptor {  

	private final Object target;

	// ... 
	
    @Override  
    public Object intercept(Object obj, Method method, Object[] args, MethodProxy methodProxy) throws Throwable {  
        return methodProxy.invoke(target, args);
    }}
```

프록시에 적용하고자 하는 로직은 MethodInterceptor를 구현해 적용하면 된다. 

#### Proxy 생성 

```java
Enhancer enhancer = new Enhancer();  
enhancer.setSuperclass(ConcreteService.class);  
enhancer.setCallback(new TimeMethodInterceptor(target));  
ConcreteService proxy = (ConcreteService) enhancer.create();
```
- CGLIB는 Enhancer를 사용해 프록시를 생성한다. 
- `setSuperclass()`를 통해 상속받을 구체클래스를 지정한다. 
- `setCallback()`을 통해 프록시에 적용할 로직을 할당한다.

