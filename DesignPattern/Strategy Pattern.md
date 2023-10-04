변하지 않는 부분을 Context에 두고, 변하는 부분을 Strategy라는 인터페이스를 만들어 해당 인터페이스를 구현하도록 해 문제를 해결하는 디자인 패턴이다. (상속이 아닌 위임으로 문제를 해결한다.)

##### Structure
![[Pasted image 20231004171414.png]]

##### 예제 코드 
**필드에 Strategy를 저장**

```java
@Slf4j  
public class ContextV1 {  
  
    private Strategy strategy;  
  
    public ContextV1(Strategy strategy) {  
        this.strategy = strategy;  
    }  
    public void execute() {  
        long startTime = System.currentTimeMillis();  
        strategy.call();    // 위임  
        long endTime = System.currentTimeMillis();  
        long resultTime = endTime - startTime;  
        log.info("resultTime={}", resultTime);  
    }}

---

public interface Strategy {  
    void call();  
}

---

@Slf4j  
public class StrategyLogic1 implements Strategy{  
    @Override  
    public void call() {  
        log.info("비즈니스 로직1 실행");  
    }}
```

**파라미터에 Strategy를 전달받음**

```java
@Slf4j  
public class ContextV2 {  
  
    public void execute(Strategy strategy) {  
        long startTime = System.currentTimeMillis();  
        strategy.call();    // 위임  
        long endTime = System.currentTimeMillis();  
        long resultTime = endTime - startTime;  
        log.info("resultTime={}", resultTime);  
    }}

--- 

public interface Strategy {  
    void call();  
}

---

@Slf4j  
public class StrategyLogic1 implements Strategy{  
    @Override  
    public void call() {  
        log.info("비즈니스 로직1 실행");  
    }}
```

Strategy 방식은 크게 두가지로 나뉜다. 
* 필드에 Strategy를 저장하는 방식
* 파라미터로 Strategy를 전달받는 방식

필드에 Strategy를 저장하는 방식
> Constructor로 Strategy를 받기 때문에, 선 조립 후 실행 방식의 특징을 지닌다. 
> Context 실행 시점에는 이미 조립이 끝나있기 때문에, 바로 사용이 가능하다. 

파라미터로 Strategy를 전달받는 방식
> Method의 파라미터로 Strategy를 받기 때문에 실행시 마다 유연하게 Strategy를 바꿔 사용할 수 있다.
> 실행 시 마다 