### *02.03_ Today I learned_ Java*

## Java Class의 구성 멤버

![img](https://search.pstatic.net/common/?src=http%3A%2F%2Fcafefiles.naver.net%2FMjAxNzA0MTdfMTk3%2FMDAxNDkyNDA2NzU5MDYy.ZGr03FmUfos1jle-U2ybpvL1pVSlwGfdkKD0OP5J9NEg.wZsiTqUL_uMMqSfngUeU1TZhvjQr6b8n0wGEclXFhRYg.PNG.gus9769%2FKakaoTalk_20170417_142032266.png&type=sc960_832)

![image-20210212181534247](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210212181534247.png)

#### 1. Field_필드

> 객체의 고유 데이터, 부품 객체, 상태 정보를 저장하는 곳
>
> 선언 형태는 변수(Variable)과 비슷하지만, 필드를 변수라고 부르지 않는다. 변수는 생성자와 메소드 내에서만 사용되고 생성자와 메소드가 실행 종료되면 자동 소멸된다. 하지만 필드는 생성자와 메소드 전체에서 사용되며 객체가 소멸되지 않는 한 객체와 함께 존재한다.

#### 2. Constructor_생성자

> 생성자는 new 연산자로 호출되는 특별한 중괄호`{}`블록이다. 
>
> 생성자는 객체 생성 시 초기화를 담당한다. 
>
> 생성자는 메소드와 비슷하게 생겼지만, **클리스 이름**으로 되어 있고, 리턴 타입이 없다.

#### 3. Method_메소드

> 메소드는 객체가 동작하는 부분
>
> 어떠한 특정 작업을 수행하기 위한 **명령문의 집합**
>
> 모듈화로 인해 전체적인 **코드의 가독성이 향상**된다. 
>
> 또한 프로그램에 문제가 발생하거나 기능의 변경이 필요할 때도 **손쉽게 유지보수**를 할 수 있다.
>
> 메소드는 필드를 읽고, 수정하는 역할도 있지만, 다른 객체를 생성해서 다양한 기능을 수행하기도 한다.



![img](https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles.naver.net%2FMjAyMDA1MDNfMjI3%2FMDAxNTg4NDY2MTY5MjE4.V2L4j6VUjPBx_pqVrn2ob8WSYQ0QPEEH4edqdFfmHBEg.rp62188oBqQiPWO-W4QcfRH83OADAFm4A95l530oV1sg.PNG.wnsghks1017%2F%25BC%25B3%25B8%25ED22222.png&type=sc960_832)

​																	*1. 접근 지정자 / 2. 클래스 선언 / 3. 클래스명 / 4.필드 / 5. 메소드*







## OOP(object Oriented Programming)_객체 지향 프로그래밍의 3대 Concept

#### 1. **encapsulate**_캡슐화

> 객체의 필드, 메소드를 하나로 묶고 실제 구현 내용을 감주는 것
>
> 외부 객체는 객체 내부의 구조를 알지 못하며 객체가 노출해서 제공하는 필드와 메소드만 이용할 수 있다.
>
> **필드와 메소드를 캡슐화하여 보호하는 이유는 외부의 잘못된 사용으로 인해 객체가 손상되지 않도록 하기 위해서다. (보안, data 보호)**
>
> *[ Access Modifier (접근 지정자) ]*
>
> | 접근 지정자 | 설명                                                         |
> | ----------- | ------------------------------------------------------------ |
> | private     | 같은 package 내에서도 접근 불가, 자기 class내에서만 접근 가능 |
> | default     | 같은 package 내에서만 접근 가능                              |
> | protected   | 다른 package 에서도 상속 관계면 접근 가능                    |
> | public      | Class와 method도 public이기 때문에 다른 package에서도 접근 가능 |



#### 2. Inheritance_상속

> 상위 객체의 필드와 메소드를 하위 객체도 사용할 수 있다. 
>
> **개발 속도를 향상시키며, 반복된 코드를 줄일 수 있다.**
>
> 모든 객체는 `Object`가 루트이니 어떤 객체던지 최상위 부모는 `Object`이다.
>
> * `extends` : 단일 상속(단일 부모), 명확하게 계층을 잡는다.
>
>   ```java
>   public class A{
>       int field1:
>       void method1() {...}
>   }
>   
>   ​```
>   public class B extents A{ //extends A: A를 상속한다.
>       String field2;
>       void method2(){...}
>   }    
>   ```
>
>   
>
> * `gettter` and `setter` : 객체 지향 프로그래밍에서는 객체 안의 필드 값을 직접 수정하거나 읽지 않고 메소드를 통해 관리하는데, 이러한 것을  getter and setter 라고 한다.
>
> > **data 상속은 지양, method 상속은 지향**



#### 3. Polymorphism_다형성

> 같은 타입이지만 실행 결과가 다양한 객체를 이용할 수 있는 성질
>
> 하나의 타입에 여러 객체를 대입함으로써 다양한 기능을 이용할 수 있도록 해준다.
>
> **객체를 부품화시키는 것이 가능하며, 유지보수가 용이해진다.**
>
> 1.  Polymorphic Variable_다형적 변수 :  super type으로 선언된 변수
>
>    ```java
>    public void String(Shape S){ //정의
>           } //여기서 S가 다형적 변수, Circle, Rectangle, Triangle 모두 shape의 하위 객체를 가리키는 변수
>    ```
>   ```
> 
> 2.  **Override**_재정의 : 상속관계에서 부모의메소드를 재정의해서 **자식클래스에 맞게 사용하는 것**
> 
>    Super의 메소드를 sub에서 다시 정의하는 것
> 
>    **`shadow effect`를 우회하기 위함_ 확장성, 성능 향상을 위해서 **
> 
>    * `shadow effect` : super type으로 선언된 객체는 그 super type으로만 취급한다. 하위 type 멤버는 가려지는 효과
> 
>    ```java
>    public class Animal{
>        void eat() {
>            System.out,println("Animal이 먹습니다.");
>        }
>        void sleep(){
>            System.out.println("Animal이 잡니다.");
>        } 
>    }
>   ```
>
>    ```java
>    public class Dog extends Animal{
>        void eat(){
>           System.out.println("Dog가 먹습니다.");
>        }
>        void sleep(){
>            System.out.println("Dog가 잡니다.");
>        }
>    }
>    ```
>
>    위와 같이 Dog 클래스는 Animal 클래스에 의해 상속받고 있고, 같은 메소드를 사용하지만, 오버라이딩으로 다시 정의를 했다.
>
>    자식 클래스에 맞게 "Dog가 먹습니다." 라고 재정의를 한 것이다.
>
>    ```java
>   public class OverRideTest{
>        public static void main(String[] args){
> 
>            Animal myAnimal = new Animal();
>            Dog myDog = new Dog();
> 
>            myDog.eat();
>            myDog.sleep();
>        }
>    }
>    ```
>
>    이렇게 객체를 생성해서 메소드를 실행하면 아래와 같이 결과가 나온다.
>
>    ![image-20210203201315983](https://postfiles.pstatic.net/MjAyMDA2MDRfMjMz/MDAxNTkxMjY3NTAzNjEw.rusWGOsdGQ09rkZbZ5ukQgUzywW0JAVP_G-fmFtzb-Eg.y9L7y7_GDY-tpzMWGI4sP-9XjtSDJPT107oaK82lnesg.PNG.wnsghks1017/%EC%98%A4%EB%B2%84%EB%9D%BC%EC%9D%B4%EB%93%9C_33.png?type=w773)
>
> 
>
>    이처럼 부모 클래스의 메소드를 수정할 일이 있거나 자신에게 맞게 바꾸기 위해 사용하는데, 메소드의 이름이나 구조를 변경해서는 안 되고 실행되는 블록 `{}` 만 고쳐 써야 한다. **리턴 타입, 매개변수 개수, 데이터 타입 이름은 동일해야 한다.**
>
>    오버라이드는 **상속관계**에서 사용된다는 것을 기억하자.
>
> 3.  **Overload**_오버로드 : **한 클래스 내에서 같은 이름의 메소드가 다시 존재**하는 것
>
>    원래는 한 클래스에 같은 이름의 메소드를 사용하는 것은 불가능하다. 하지만 오버로드 조건에 맞춘다면 같은 이름의 메소드를 여러 번 사용 가능하다.
>
>    * 조건
>
>      **메소드의 매개변수의 개수 또는 데이터 타입이 다르면 오버로드 조건을 만족한다.**
>
>      하지만 리턴타입만 다른 것은 안 된다.(리턴 타입은 같아도 되고, 달라도 된다. 상관없음.)
>
>      ```java
>     public class OverLoadTest{
>          int add(int a, int b) {
>             return a+b;        
>          }
>          int add(int a, int b, int c){ //매개변수 개수가 다를 때 오버로드 성립
>              return a+b+c;
>          }
>          double add(double a, double b){ //매개변수 데이터 타입이 다를 때 오버로드 성립
>              return a+b;
>          }
>      }
>      ```
