# IOC/DI
: 제어의 역전/의존성 주입

## 👉 스프링 없이 의존성 주입
✔ 1. 생성자를 통한 의존성 주입
```
public class Car{
    Tire tire;

    public Car(Tire tire){
        this.tire = tire;
    }
}

public static void main(String[] agrs){
    Tire tire = new KoreaTire();
    Car car = new Car(tire);
}
```
이렇게 생성자를 통해 의존성을 주입받게 되면, 어떠한 종류의 tire 객체를 받더라도 정삭적으로 작동할 수 있다.

<br/>
✔ 2. 속성을 통한 의존성 주입
```
Tire tire = new KoreaTire();
Car car = new Car();
car.setTire(tire);
```
처음 객체를 생성한 뒤에도 Tire객체를 바꾸고자 할 때, 언제든 변경 가능하다는 장점이 있다.


<br/><br/>

## 👉 스프링을 통한 의존성 주입
✔ 1. XML 파일 사용
```
<xml>
    <bean id="tire" class="expert002.KoreaTire"></bean>
    <bean id="americaTire" class="expert002.americaTire"></bean>
</xml>
```

```
ApplicationContext context = new ClassPathXmlApplicationContext("expert002.xml", Driver.class);
Tire tire = (Tire)context.getBean("tire");
Car car = (Car)context.getBean("car");
car.setTire(tire);
```
![020](https://user-images.githubusercontent.com/49690185/105181533-41e5aa80-5b6f-11eb-8d48-a3b7090356f3.png)
xml을 통해 의존성을 주입받게 될 경우 재컴파일/재배포 하지 않아도 XMl 파일만 수정하면 프로그램의 실행 결과를 바꿀 수 있다.

✔ 2. 스프링 설정 파일(XML)에서 속성 주입
```
<xml>
    <bean id="tire" class="expert002.KoreaTire"></bean>
    <bean id="americaTire" class="expert002.americaTire"></bean>
    <bean id="car" class="expert002.Car">
        <property name="tire" ref="koreaTire"></property>
    </bean>
</xml>
```
```
ApplicationContext context = new ClassPathXmlApplicationContext("expert002.xml");
Car car = context.getBean("car", Car.class);
```
![023](https://user-images.githubusercontent.com/49690185/105181609-5e81e280-5b6f-11eb-9644-1f73ed1f5748.png)


✔ 3. @Autowired를 통한 속성 주입
```
import org.springframework.beans.factory.annotation,Autowired;

@Autowired
Tire tire;
```
![026](https://user-images.githubusercontent.com/49690185/105181749-896c3680-5b6f-11eb-857a-2ca25fec8ade.png)

스프링이 설정 파일을 보고 자동으로 속성의 설정자 메서드에 해당하는 객체를 전달해준다.
|Car.java|@Autowired Tire tire;|
|-|-|
|expert.xml|&lt;bean id="usaTire" class="AmericaTire"&gt;&lt;/bean&gt;|
다음과 같이 id값이 있든 없든 한개의 Bean이 존재한다면 의존성을 주입 받을 수 있다. 하지만, 두 개 이상의 Bean이 있을 경우에는 id값을 작성해서 어떠한 Bean을 주입받을지 명시해주어야한다.

✔ 4. @Resource를 통한 속성 주입
```
@Resource
Tire tire;
```
- @Resource는 자바 표준 어노테이션이다.
- @Autowired는 스프링의 어노테이션이기 때문에, 스프링 프레임워크를 사용하지 않는다면 사용할 수 없다.
- @Autowired는 xml파일에서 type과 id 가운데 매칭 우선순위는 type이 높다
- 하지만 @Resource는 매칭 우선순위가 id가 더 높다.





<br/><br/>
>Reference:
>「스프링 입문을 위한 자바 객체 지향의 원리와 이해」 - 김종민
