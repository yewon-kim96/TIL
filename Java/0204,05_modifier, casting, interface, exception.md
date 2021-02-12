​    

# 9,10일차(20.02.04~02.05)_ Java

> [K-Digital] 온·오프 연계 AI활용 지능형 서비스 개발 수업 9, 10일차



## 1. Modifier (지정자)

### 1.1 접근 지정자 (Access modifier)

	1. private
	2. (default)
	3. protected
	4. public

### 1.2 사용 지정자 (Usage modifier)

#### 1.2.1 static

> 클래스에 고정된 멤버로서 객체 생성 없이도 사용할 수 있는 필드와 메소드를 의미
>
> * 유일하게 이름으로 참조할 수 있다.
> * static 사용을 지양 -> **메모리 비효율, 꼭 공유해야 되는 데이터가 있을 때만 사용**
>
> >1.  class 앞 : **inner class**에서만!
> >2.  data 앞 : 공유하는 데이터
> >3.  method 앞 : 공유하는 데이터지만, 별 이득이 없다.
> >
> >```  java
> >package static_final;
> >
> >public class Earth {
> >	static final double EARTH_RADIUS = 6400;
> >	static final double EARTH_SURFACE_AREA;
> >	
> >	static {
> >		EARTH_SURFACE_AREA = 4 * Math.PI * EARTH_RADIUS * EARTH_RADIUS;				
> >	}
> >
> >}
> >
> >package static_final;
> >
> >public class EarthExample {
> >
> >	public static void main(String[] args) {
> >		System.out.println("지구의 반지름 : " + Earth.EARTH_RADIUS + " km");
> >		System.out.println("지구의 표면적 : " + Earth.EARTH_SURFACE_AREA + " km^2");
> >	}
> >}
> >```
>
> 
>
> * 객체 생성 안하고 main을 수행하기 위해 static을 사용
>   * JVM도 외부 프로그램이기 때문에 main이 **public**이어야 한다.

#### 1.2.2 final

> 변경 없이 고정해놓고 사용 ex) String
>
> > 1.  class  앞 : **상속 불가**
> >
> > ```java
> > final class Animal{
> >     String word = "동물이다.";
> >     public void println() {
> >         System.out.println("Animal은 " + word);
> >     }
> >  }
> > 
> > class Bird extends Animal {
> >     //final 인 Animal을 상속할 수 없기 때문에 컴파일 에러
> > } 
> > ```
> >
> > 2. data 앞 :  상수, **값 변경 불가**
> >
> > ```java
> > package final_field;
> > //final 필드 선언과 초기화
> > public class Person {
> > 	final String nation = "Korea";
> > 	final String ssn;
> > 	String name;
> > 	
> > 	public Person(String ssn, String name) {
> > 		this.ssn = ssn;
> > 		this.name = name;
> > 	}
> > }
> > 
> > package final_field;
> > 
> > public class PersonExample {
> > 
> > 	public static void main(String[] args) {
> > 		Person p1 = new Person("123456-1234567", "계백");
> > 		
> > 		System.out.println(p1.nation);
> > 		System.out.println(p1.ssn);
> > 		System.out.println(p1.name);
> > 
> > //		p1.nation ="usa";  //final 필드값은 수정 불가
> > //		p1.ssn = "654321-7654321";
> > 		p1.name ="을지문덕";
> > 		System.out.println(p1.name);
> > 	}
> > }
> > ```
> >
> > 3. method 앞 : **오버라이딩 불가** 
> >    * 오버라이딩 : 상속관계에서 부모의 매소드를 재정의해서 자식 클래스에 맞게사용하는 것, super의 메소드를 sub에서 다시 정의하는 것
> >
> > ```java
> > final class Animal{
> >     String word = "동물이다.";
> >     final public void println() {
> >         System.out.println("Animal은 " + word);
> >     }
> >  }
> > 
> > class Bird extends Animal {
> >     public void printI() { //final인 메소드를 오버라이딩 할 수 없어 컴파일 에러 발생
> >         System.out.println("Bird는 " + word);
> >     }
> > } 
> > ```

#### 1.2.3 abstract

> 객체 생성 불가 -> 상속으로만 사용
>
> > 1.  class 앞 : 객체 생성 불가  ==  상속으로만 사용
> >    * 추상 클래스가 부모이고 실체 클래스가 자식으로 구현되어 실체 클래스는 추상 클래스의 모든 특성을 물려받고, 추가적인 특성을 가질 수 있다.
> >    * 추상 클래스는 **new 연산자를 사용해서 인스턴스를 생성시키지 못한다.**
> >    * 사용목적 : 공통적인 필드와 메소드는 추상클래스에 모두 선언해두고, 실체 클래스마다 다른 점만 실체 클래스에 선언하면, 실체 클래스 작성 시간 단축
> >
> > ```java
> > package abstract_;
> > 
> > //추상 클래스
> > public abstract class Phone { 
> > 	//필드
> > 	public String owner;
> > 	
> > 	//생성자
> > 	public Phone(String owner) {
> > 		this.owner = owner;
> > 	}
> > 	
> > 	//메소드
> > 	public void turnOn() {
> > 		System.out.println("폰 전원을 켭니다.");
> > 	}
> > 	public void turnOff() {
> > 		System.out.println("폰 전원을 끕니다.");
> > 	}
> > }
> > 
> > package abstract_;
> > 
> > //실체 클래스
> > public class SmartPhone extends Phone {
> > 	//생성자
> > 	public SmartPhone(String owner) {
> > 		super(owner);
> > 	}
> > 	
> > 	//메소드
> > 	public void internetSearch() {
> > 		System.out.println("인터넷 검색을 합니다.");
> > 	}
> > }
> > 
> > 
> > package abstract_;
> > 
> > 
> > public class PhoneExample {
> > 
> > 	public static void main(String[] args) {
> > 		//Phone phone = new Phone();
> > 		
> > 		SmartPhone smartPhone = new SmartPhone("홍길동");
> > 		
> > 		smartPhone.turnOn();
> > 		smartPhone.internetSearch();
> > 		smartPhone.turnOff();
> > 
> > 	}
> > 
> > }
> > ```
> >
> > 2. method 앞 : 구현 블럭 없음이라는 뜻이다.
> >    * abstract method 가 하나라도 있으면 class는 abstract이어야 한다.
> >    * 해당 class를 상속받으면 overriding 필수
> >
> > ```java
> > package abstract_overriding;
> > 
> > //추상클래스 
> > public abstract class Animal {
> > 	public String kind;
> > 	
> > 	public void breathe() {
> > 		System.out.println("숨을 쉽니다.");
> > 	}
> > 	
> > 	public abstract void sound(); //추상 메소드 선언
> > 
> > }
> > 
> > package abstract_overriding;
> > //추상 메소드 오버라이딩
> > public class Dog extends Animal {
> > 	public Dog() {
> > 		this.kind = "포유류";	
> > 	}
> > 	
> > 	@Override //추상 메소드 재정의
> > 	public void sound() {
> > 		System.out.println("멍멍");
> > 	}
> > }
> > 
> > package abstract_overriding;
> > //추상 메소드 오버라이딩
> > public class Cat extends Animal {
> > 	public Cat() {
> > 		this.kind = "포유류";		
> > 	}
> > 	
> > 	@Override //추상 메소드 재정의
> > 	public void sound() {
> > 		System.out.println("야옹");
> > 	}
> > 
> > }
> > ```
> >
> > 3. data 앞에는 사용하지 못함





---



## 2. Casting 

### 2.1 형변환 (Casting)

> 변수의 자료형(Data type)을 다른 자료형으로 변환하는 것
>
> * 자바에서는  int, long과 같은 기본 타입 변수뿐만 아니라 객체를 참조하는 변수도 상속 관계에 있는 부모 클래스와 자식  클래스 간에 형변환이 가능하다.
> * 여기서 참조 변수의 자료형이 자식 클래스에서 부모 클래스로 변환되는 것을 업캐스팅(Upcasting)이라고 하고, 반대로 부모 클래스에서 자식 클래스로 변환되는 것을 다운캐스팅(Downcasting)이라고 한다.

#### 2.1.1 업캐스팅 (Upcasting)

> 자바에서 자식 클래스는 부모 클래스에서 정의한 맴버 변수와 메소드를 모두 상속받았기 때문에 
>
> 부모 클래스의 자료형으로 변환될 수 있는데 이를 업캐스팅이라고 한다.
>
> * **업캐스팅을 하게 되면 부모 클래스로부터 상속받은 멤버 변수와 메소드에는 접근이 가능하지만, 자식 클래스에서 새롭게 정의한 멤버 변수와 메소드에는 접근할 수 없다.**

#### 2.1.2. 다운캐스팅 (Downcasting)

> 다운캐스팅이란 부모클래스로 형변환되었던 객체의 자료형을 자식 클래스로 복원해주는 것을 말한다.
>
> * 객체는 부모 클래스로 형변환되면서 잃어버렸던 고유한 특성, 즉 **자식 클래스에서 새롭게 정의한 멤버 변수와 메소드에 다시 접근할 수 있게 된다.**

```java
public class Person { //부모 클래스 타입
    public String name;
    public Person(String name) {
        this.name = name;
    }
    public void printName() {
        System.out.println("My name is "+ name + ".");
    }

}

public class Student extends Person { //자식 클래스 타입
    public Student(String name){
        super(name);
    }
    public void introduce() {
        super.printName();
        System.out.println("And I'm studying.");
        
    }
    
}

public class CastingTest {
    public static void main(String[] args) {
        Person person = new Person("Joshua");
        Student student = new Student("Justin");
        
        Person upcast = new Student("Jonathan"); //업캐스팅
        Student downcast = (Student) upcast; //다운캐스팅 
        
        person.printName();
        System.out.println("---");
        
        student.printName();
        student.introduce();
        System.out.println("---");
        
        upcast.printName(); 
        //upcast.introduce(); -> 컴파일 에러 발생
        System.out.println("---");
        
        downcast.printName();
        downcast.introduce();
    }
}
```

![image-20210208144341337](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210208144341337.png)

### 2.2 instanceof

> 객체의 데이터 타입을 확인하기 위해서 사용하는 연산자
>
> * 사용법은 아래와 같으면, [객체 참조 변수]의 데이터 타입이 피연산자인 [클래스]와 동일하거나 [클래스]로부터 상속받은 클래스안 경우에는 true를, 기타의 경우에는 false를 반환한다.
> * 일반적으로 instanceof는 부모 클래스로 업캐스팅된 객체를 다운캐스팅하기 전에 클래스의 데이터 타입을 확인하기 위한 목적으로 많이 사용된다.
>
> ```java
> [참조 변수] instanceof [클래스명]
> ```
>
> ```java
> public class Person { //부모 클래스 타입
>     public String name;
>     public Person(String name) {
>         this.name = name;
>     }
>     public void printName() {
>         System.out.println("My name is "+ name + ".");
>     }
> }
> 
> public class Student extends Person { //자식 클래스 타입
>     public Student(String name){
>         super(name);
>     }
>     public void introduce() {
>         super.printName();
>         System.out.println("And I'm studying.");
>         
>     }
> }
> 
> public class Teacher extends Person{
>     public Teacher(String name) {
>         super(name);
>     }
>     public void introduce() {
>         super.printName();
>         System.out.println("And I am teaching students.");
>     }
> }
> 
> import java.util.Random;
> public class InstanceOfTest {
>     public static void main(String[] args) {
>         Random random = new Random();
>         Person person;
>         
>         if (random.nextBoolean() == true) {
>             person = new Teacher("Sullivan");
>         } else {
>             person = new Student("Helen");
>         }
>         if (person instanceof Teacher) {
>             Teacher teacher = (Teacher) person;
>             teacher.introduce();
>         } else {
>             Student student = (Student) person;
>             student.introduce();
>         }
>     
>     }
> }
> ```
>
> ![image-20210208170711566](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210208170711566.png)



---



## 3. Java Program 단위

### 3.1 class 기본

```java
public class Name{ //접근지정자_class_class이름
    //행위;
}
```

### 3.2 Enum (열거)

> public + static + final 로 구현 -> 상수를 표현하는 함수의 단위
>
> *  **코드의 가독성 증가**
>
> * enum 하나하나를 객체로 본다.
> * emum의 이름이 type
>
> ```java
> class Week extends {
> 	public static final char MON = '월‘
> 	public static final char TUE = '화‘
> 	public static final char WED = '수‘
> 	public static final char THU = '목‘
> 	public static final char FRI = '금‘
> 	public static final char SAT = '토‘
> 	public static final char SUN = '일‘ // 이 표현을 살짝 바꾼게 enum
> }
> ```
>
> ```java
> public enum Week {
>     MON, TUE, WED, TUR, FRI, SAT, SUN;
> }
> ```

### 3. 3 Interface ( 인터페이스)

> 다중 상속을 위한 프로그램 단위
>
> * 인터페이스는 객체의 교환성을 높여주기 때문에 다형성을 구현하는 매우 중요한 역할을 한다.
> * 개발 코드 측면에서는 코드 변경 내용 없이 실행 내용과 리턴값을 다양화할 수 있다는 장점
> * 클래스는 필드, 생성자, 메소드를 구성 멤버로 가지는데 비해, 인터페이스는 상수와 메소드만을 구성 멤버로 가진다.
>   * 인터페이스는 객체로 생성할 수 없기 때문에 **생성자를 가질 수 없다.**
> * `implements` : 뒤로 다른 인터페이스를 받아서 다수의 다수의 인터페이스 타입으로 사용가능
> * 인터페이스도 다른 인터페이스를 상속할 수 있다. 인터페이스는 클래스와는 달리 다중 상속을 허용한다.
>
> ```java
> public class 구현 클래스명 implements 인터페이스명 {
>     //인터페이스에 선언된 추상 메소드의 실체 메소드 선언
> }
> ```
>
> ```java
> package interface_;
> //인터페이스
> public interface Tire {
> 	public void roll(); //roll() 메소드 호출 방법 설명
> }
> 
> 
> public class HankookTire implements Tire {
> 	@Override
> 	public void roll() { //Tire 인터페이스 구현
> 		System.out.println("한국 타이어가 굴러갑니다.");
> 	}
> }
> 
> public class KumhoTire implements Tire { 
> 	@Override
> 	public void roll() { //Tire 인터페이스 구현
> 		System.out.println("금호 타이어가 굴러갑니다.");
> 	}
> }
> 
> public class Car {
> 
> 	//인터페이스 타입 필드 선언과 초기 구현 객체 대입
> 	Tire frontLeftTire = new HankookTire();
> 	Tire frontRightTire = new HankookTire();
> 	Tire backLeftTire = new HankookTire();
> 	Tire backRightTire = new HankookTire();
> 
> 	void run() { //인터페이스에서 설명된 roll() 메소드 호출
> 		frontLeftTire.roll();
> 		frontRightTire.roll();
> 		backLeftTire.roll();
> 		backRightTire.roll();		
> 	}
> }
> 
> public class CarExample {
> 
> 	public static void main(String[] args) {
> 		Car myCar = new Car();
> 
> 		myCar.run();
> 
> 		myCar.frontLeftTire = new KumhoTire();
> 		myCar.frontRightTire = new KumhoTire();
> 
> 		myCar.run();
> 
> 	}
> 
> }
> ```
>
> ![image-20210208051036532](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210208051036532.png)
>
> ```java
> package interface_inheritance; //인터페이스 상속
> //부모 인터페이스
> public interface InterfaceA {
> 	public void methodA();
> 
> }
> 
> package interface_inheritance;
> //부모 인터페이스
> public interface InterfaceB {
> 	public void methodB();
> 
> }
> 
> package interface_inheritance;
> //하위 인터페이스
> public interface InterfaceC extends InterfaceA, InterfaceB { //인터페이스 상속
> 	public void methodC();
> }
> 
> 
> public class ImplementationC implements InterfaceC { //하위 인터페이스 구현
>     public void methodA() {
>         System.out.println("ImplementationC-methodA() 실행"); //InterfaceA와
>     }
>     
>     public void methodB() {
>         System.out.println("ImplementationC-methodB() 실행"); //InterfaceB의 실체 메소드도 있어야 한다.
>     }
>     
>     public void methodC() {
>         System.out.println("ImplementationC-methodC() 실행");
>     }    
> }
> 
> 
> public class Example { //호출 가능 메소드
>     public static void main(String[] args) {
>         ImplementationC impl = new ImplementationC();
>         
>         InterfaceA ia = impl;
>         ia.methodA();
>         System.out.println(); //InterfaceA 변수는 methodA()만 호출 가능
>         
>         InterfaceB ib = impl;
>         ia.methodB();
>         System.out.println(); //InterfaceB 변수는 methodB()만 호출 가능
>         
>         InterfaceC ic = impl;
>         ia.methodC();
>         System.out.println(); //InterfaceC 변수는 methodA(), methodB(), methodC() 모두 호출 가능
>     }
> }
> ```
>
> ![image-20210212175555561](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210212175555561.png)



---



## 4. Exception (예외)

> 프로그래밍 오류를 잡고 실행을 계속할 수 있는 기법

### 4.1 try ~ catch ~ finally

> ```java
> try {
>     //예외가 발생할 가능성이 있는 코드
> } catch(Exception1 e1) {
>     //예외1이 발생했을 때 수행해야 하는 코드
> } catch(Exception2 e2) {
>     //예외2가 발생했을 때 수행해야 하는 코드
> } finally {
>     //예외 발생 여부에 상관없이 무조건 실행해야 하는 코드
> }
> ```
>
> * try 블럭은 예외가 발생할 가능성이 있는 코드를 기술하는 곳이다. 
> * try 블럭은 최조한 하나 이상의 catch 블럭을 가지며, 이렇게 정의된 catch 블럭을 통해 try 블럭에서 발생한 예외를 처리한다.
> * catch 블럭은 try 블럭 다음에 오며, try 블럭에서 발생 가능한 예외의 종류만큼 선언할 수 있다. 즉, try 블럭에서 발생 가능한 예외가 1개인 경우에는 1개의 catch 블럭을, 2개인 경우엔 2개의 catch 블럭을 정의하여 각각에 대해 예외 처리를 수행할 수 있다.
> * finally 블럭은 선택 구문으로 반드시 있어야 하는 것은 아니다. 단, finally 블럭을 선언하면 이 블럭 안에 기술된 코드는 예외 발생 또는 예외 처리 유무에 상관없이 무조건 실행된다. 따라서 보통은 데이터베이스 또는 파일을 사용 중 오류가 발생했을 때, DB와의 연결을 끊거나 파일을 닫는 것과 같이 오류가 발생하더라도 반드시 수행되어야 하는 구문에 대해 사용한다.

### 4.2 throws 

> 메소드를 호출한 곳으론 예외를 떠넘기는 방법
>
> 에러를 대비할 수 있는 기회를 준다.
>
> ```java
> public void performSomeAction() throws Exception1, Exception2, ... {
>     //메소드의 실행 코드
>     //발생 가능한 예외 Exception1, Exception2등에 대해 예외 처리를 수행하지 않고 throws를 이용하여 메소드를 호출한 곳으로 예외처리를 이관한다.
> }
> ```
>
> ```java
> package test.exception2;
> 
> public class Calculator {
> 	public int divide(int x, int y) throws MyException { //throw 방법
> 		
> 		int z=0;
> 		if(y==0) {
> 			throw new MyException("y를 0으로 입력하지 마세요...");
> 		}
> 			z=x/y;
> 		return z;
>     }
> }
> 
> public class MyException extends Exception { //MyException class를 따로 만드는 이유는 메세지를 전달해주기 위해서, 만들지 않으면 null값 이 나온다.
> 
> 	public MyException(String message) {
> 		super(message);
> 		
> 	}
> }
> 
> public class Test {
> 
> 	public static void main(String[] args) {
> 	
> 		Calculator c=new Calculator();
> 		int result=0; //local 변수이므로 반드시 초기화해줘야 한다.
> 		try {
> 			result = c.divide(100, 0);
> 		} catch (MyException e) {
> 			
> 			System.out.println(e.getMessage());
> 		}finally {//반드시 실행해야되야 된다.
> 		System.out.println(result);
> 		
> 		System.out.println("아주 중요한 일 시작...");
> 	}
> 
> 	}
> }
> ```
>
> ![image-20210208093604546](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210208093604546.png)



