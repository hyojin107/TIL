# AOP
: Aspect Oriented Programming의 약어로써 관점 지향 프로그래밍을 말한다.

- Spring AOP 는 interface 기반이다.
- Spring AOP 는 Proxy 기반이다.
- Spring AOP 는 runtime 기반이다.

<img width="410" alt="다운로드" src="https://user-images.githubusercontent.com/49690185/105354078-66a35600-5c33-11eb-83a2-cd2dc61b60db.png">

before()와 after()처럼 공통적으로 나타내는 코드를 _**횡단 관심사**_ 라고 한다.
그리고 getBoards()와 같이 중간에 들어간 코드를 _**핵심관심사**_ 라고 한다.

## AOP 용어
|용어|영한 사전|
|-|-|
|Aspect|관점, 측면, 양상|
|Advisor|조언자, 고문|
|advice|조언, 충고|
|JoinPoint|결합점|
|Pointcut|자르는 점|

✔ **Pointcut**
- Aspect적용 위치 지정자
- 횡단 관심사를 적용할 타깃 메서드를 선택하는 지시자
```
@Aspect
public class MyAspect{
    @Before("execution(runSomething())")
    public void before(JoinPoint joinPoint){...}
}
```
위의 예시에서는 runSomething이 Pointcut이다.

✔ **JoinPoint**
- Pointcut은 JoinPoint의 부분 집합이다.
- Aspect 적용이 가능한 모든 지점을 말한다. (메소드 단위로만 지정)
- _호출된 객체의 메서드이다._

✔ **Advice**
- pointcut에 언제, 무엇을 적용할지 정의한 메서드다.
- 타깃 객체의 타깃 메서드에 적용될 부가 기능

✔ **As[ect**
- 여러 개의 Advice와 여러 개의 Pointcut의 결합체를 의미
- Aspect = Advice들 + Pointcut들
- Aspect = 언제, 무엇을 + 어디에



<br/><br/>
> Reference: 
>「스프링 입문을 위한 자바 객체 지향의 원리와 이해」 - 김종민
> https://jojoldu.tistory.com/71
