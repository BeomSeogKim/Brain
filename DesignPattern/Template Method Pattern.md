Template 에 공통된 기능들을 모아두고, 변경되는 부분들은 Method 를 호출해 처리하는 방식의 디자인 패턴.

##### Structure
![[Pasted image 20231004170106.png]]

##### 예제 코드 
```java
@Slf4j  
public abstract class AbstractTemplate {  
  
    public void execute() {  
        long startTime = System.currentTimeMillis();  
        call();  
        long endTime = System.currentTimeMillis();  
        long resultTime = endTime - startTime;  
        log.info("resultTime={}", resultTime);  
    }  
    
    protected abstract void call();  // abstract method -> 위임
}

--- 

@Slf4j  
public class SubClassLogic1 extends AbstractTemplate{  
    @Override  
    protected void call() {  
      log.info("비즈니스 로직1 실행");  
    }}
    
--- 

@Slf4j  
public class SubClassLogic2 extends AbstractTemplate{  
    @Override  
    protected void call() {  
      log.info("비즈니스 로직2 실행");  
    }}

```

Template Method Pattern의 경우 하위 클래스가 상위 클래스를 **상속**한다.

이로 인해 다음과 같은 단점이 존재한다. 
- 컴파일시 부모클래스와 강한 결합 발생
- 부모클래스의 기능을 사용하지 않음에도 불구하고 부모클래스의 기능을 알고 있어야 함
- 상속을 사용하기 별도의 클래스나 익명 클래스를 만들어야 하는 부분이 복잡함