# 11일차 (20.02.08)_ Java

> [K-Digital] 온·오프 연계 AI활용 지능형 서비스 개발 수업 11일차



## 1. class

### 1.1 inner class

>* 클래스 안에 클래스 정의
>
>* 이벤트를 객체마다 따로 처리해야할 때 내부 클래스를 인스턴스 변수처럼 사용
>* 내부 클래스에서는 바깥클래스의 자원을 마음대로 사용할 수 있다.
>* 바깥 클래스에서는 내부 클래스의 자원을 직접 사용할 수 없다.
>* 바깥 클래스에서 내부 클래스의 자원을 사용하려면 반드시 **객체화**를 하여 사용한다.
>
>![image-20210212182805031](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210212182805031.png)

#### 1.1.1 사용방법

>1.  외부 클래스의 객체화
>
>```java
>바깥클래스명 객체명 = new 바깥클래스생성자();
>Outer out = new Outer();
>```
>
>2.  내부 클래스의 객체화
>
>```java
>(바깥클래스명.)안쪽클래스명 객체명 = 바깥클래스객체명.new 안쪽클래스생성자(); //바깥클래스명 생략 가능
>(Outer.)Inner in = out.new Inner();
>```
>
>3. 내부 클래스의 자원 사용
>
>```java
>내부클래스객체명.변수명;
>내부클래스객체명.method명();
>```
>
>4. 예시
>
>```java
>package inner_class;
>//inner class : 클래스 안에 클래스가 정의되는 클래스
>//@예원
>
>public class UseInner {
>	int outI;
>	
>	public UseInner() {
>		System.out.println("바깥 클래스의 생성자");
>	} //UseInner
>	
>	public void outMethod() {
>		System.out.println("바깥 클래스의 method " + outI);
>//		System.out.println("안쪽 클래스의 변수 j " + j); -> 변수를 직접 접근하여 사용할 수 없다.
>//		inMethod(); -> 내부 클래스의 method를 직접 접근할 수 없다.
>	} //outMethod
>	
>	//////////////////////////// Inner Class 시작 ////////////////////////////////
>	public class Inner {
>		int j;
>		
>		public Inner() {
>			System.out.println("안쪽 클래스의 생성자");
>		} //Inner
>		
>		public void inMethod() {
>			System.out.println("안쪽 클래스의 method j = " + j);
>			System.out.println("바깥 클래스의 변수 outI = " + outI); 
>			//내부 클래스에선는 바깥 클래스의 변수에 접근하여 사용할 수 있다.
>			outMethod(); //바깥 클래스의 method 또한 사용 가능
>		}  //inMethod
>	} //class Inner
>	////////////////////////////Inner Class 끝 ////////////////////////////////
>
>	//내부 클래스를 객체화 해보기.
>	public void createInner() {
>		@SuppressWarnings("unused")
>		Inner in = this.new Inner(); //this method를 호출하는 객체의 주소로 대체
>		//this 생략 가능
>		//this.outI
>	} //createInner
>	
>	public static void main(String[] args) {
>		//1.바깥 클래스 객체화
>		UseInner ui = new UseInner();
>		
>		ui.createInner(); //2.바깥 클래스의 객체를 사용하여 내부 클래스의 객체를 생성한다.
>		
>		System.out.println("---------------------");
>		
>		//바깥 클래스명.안쪽 클래스명 객체명 = 바깥클래스객체명.new.안쪽클래스생성자();
>		//UseInner.Inner in = ui.new Inner();
>		Inner in = ui.new Inner();
>
>		in.j = 11;
>		in.inMethod(); //내부 클래스의 method에서 바깥 클래스의 변수나 method 호출
>		
>	} //main
>} //class
>```
>
>![image-20210212194604080](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210212194604080.png)

### 1.2  nested class (중첩 클래스)

> * 내부 클래스를 **static 변수**처럼 사용
>
> ![image-20210212194736839](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210212194736839.png)

#### 1.2.1 사용방법

> 1. 객체화 없이 사용
>
> ```java
> 클래스명.변수명;
> 클래스명.method();
> ```
>
> 2. 예시
>
> ```java
> package nested_class;
> //중첩 클래스 : 클래스 안에 static 클래스를 정의하는 클래스
> //@예원
> public class UseNestedOuter {
> 	int outI;  //instance 변수
> 	static int outJ; //static 변수
> 	
> 	public void outInsMethod() {
> 		System.out.println("바깥 클래스의 instance method");
> 	} //outInsMethod
> 	
> 	public static void outStaMethod() {
> 		System.out.println("바깥 클래스의 static method");
> 	} //outStaMethod
> 
> 	//////////////////// Nested class의 시작 //////////////////////////
> 	static class Inner {
> 		static int inI;
> 		
> //		public Inner() {
> //			//Nested class는 생성자를 정의하지 않는다.
> //		}
> 		
> 		public static void inMethod() {
> 			System.out.println("내부 클래스의 method");
> //			outI = 100; //static 영역에서는 instance변수 사용 불가
> //			outInsMethod(); //instance method도 사용 불가
> 			outJ = 	100;
> 			outStaMethod(); //static 변수와 static method는 사용 가능
> 		} //inMethod
> 	} //Inner
> 	//////////////////// Nested class의 끝 //////////////////////////
> 	
> 	public static void main(String[] args) {
> 		Inner.inMethod(); //내부 클래스의 method를 static 문법으로 사용할 수 있다.
> 		
> 	}//main
> } //class
> ```
>
> ![image-20210212201016472](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210212201016472.png)

### 1.3 local class

> * 클래스를 **지역변수**처럼 사용
>
> * **method 안에서만** 사용되는 클래스
>
> * JDK 1.7부터 지역변수와 paramether는 사용할 수 있으나, 값할당은 불가능
>
>   ![image-20210212205157372](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210212205157372.png)
>
>   ```java
>   package local_class;
>   //local class : method 내부에 정의하고, method 안에서만 사용되는 지역클래스 사용
>   //@예원
>   public class UseLocalOuter {
>   	int outI;
>   	
>   	public void method(int param_i, int param_j) {
>   		int locI = 10;
>   		int locJ = 20;
>   		
>   		///////////////////// 지역 클래스 시작 /////////////////////
>   		class Local {
>   			int i;
>   			
>   			public Local() {
>   				System.out.println("지역 클래스의 생성자");
>   			} //local
>   			
>   			public void locMethod() {
>   				System.out.println("지역 클래스의  method i = " + i);
>   				System.out.println("바깥 클래스의 인스턴스 변수 outI = " + outI);
>   				System.out.println("method 안의 지역변수 locI = " + locI + ", locJ = " + locJ);
>   				System.out.println("method의 매개변수 param_ i = " + param_i + ", param_j = " + param_j);
>   				//지역 클래스에서 바깥 클래스의 인스턴스 변수에 값할당은 가능
>   				outI = 34;
>   //				locI = 1;
>   //				locJ = 1; //지역변수 출력은 가능하나 값할당은 불가능
>   //				param_i = 1;
>   //				parma_j = 1; //매개변수도 출력은 가능하나 값할당은 불가능
>   			} //locMethod
>   			
>   		} //Local class
>   		///////////////////// 지역 클래스 끝 /////////////////////
>   		
>   //		locI = 1000;
>   //		param_i = 2000; 
>   		//지역 클래스 객체화
>   		
>   		Local loc = new Local();
>   		loc.i = 100;
>   		loc.locMethod();		
>   	} //method
>   	
>   	public static void main(String[] args) {
>   		UseLocalOuter ulo = new UseLocalOuter();
>   		ulo.method(2020, 11);
>   	} //main
>   
>   } //class
>   ```
>
>   ![image-20210212205328894](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210212205328894.png)

### 1. 4  anonymous inner class

>* class Arguments (method parameter에 전달하는 값)로 사용할 때
>*  method의 매개변수로 클래스나 interface가 사용되었을 때 주로 사용
>
>1. 작성법
>
>```java
>method(new 부모가될클래스생성자() {
>    자식클래스 method 선언
>    부모 method override
>}); //이름없는 클래스가 부모가 될 클래스를 부모로 하여 생성된다.
>부모클래스명 객체명 = new 부모클래스명();
>```





## 2. import

> * 외부 패키지에 존재하는 클래스를 사용할 때 선언
> * package 선언과 class 선언 사이에서 필요한 만큼 정의
> * import 선언하지 않고 외부 패키지의 클래스를 사용하려면, 클래스 앞에 모든 패키지를 기술하는 full path를 매번 기술해야 한다.
> * 패키지가 다르고 클래스의 이름이 같은 경우에는 하나만 import 가능
>
> ```java
> import 패키지명.클래스명; // 선언된 패키지 안의 특정 클래스 하나만 사요할 때
> 
> import 패키지명.*; //선언된 패키지 안의 모든 클래스를 사용할 때, 처리 시간이 오래 걸림
> ```
>
> ```java
> package import_;
> //import : 외부 패키지에 존재하는 클래스를 사용하는 방법
> //@예원
> import java.util.Date;
> import java.util.Calendar;
> import java.util.List;
> //import java.util.*; //패키지명.* -> 해당 패키지 내 모든 클래스, 인터페이스 사용가능, 권장X
> //import java.sql.Date; //다른 패키지의 Date클래스는 import 불가, 먼저 선언하면 장땡
> //따라서 소스에서 많이 사용되는 클래스를 import 처리, 적게 사용되는 클래스는 full path 처리
> 
> 
> public class TestImport {
> 	public static void main(String[] args) {
> 		
> 		Date d = new Date();
> 		Calendar cal = null;
> 		List list = null;
> 		java.sql.Date da = null;
> 		
> 		System.out.println(d);
> 		System.out.println(cal);
> 		System.out.println(list);
> 		System.out.println(da);
> 	
> 	} //main
> 
> } //class
> ```
>
> ![image-20210212213729411](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210212213729411.png)



## 3. String

> 배열은 한번 길이가 결정되면 바꿀 수 없음

### 3.1 concat() 함수

> * concat() 함수는 한 문자열 끝에 다른 문자열을 붙일 때 사용하는 함수
> * concat() 함수를 사용하지 않고서도 연산자 **+**를 사용해서 문자열 결합을 할 수 있지만, 프로그램 내에서 객체와 함께 사용할 때는 아무래도 함수를 사용하는 것이 더 편리하다.
> * 왜나하면 연산자 +를 많이 사용하면 할수록 그만큼 String 객체의 수가 늘어나기 때문에, 프로그램의 성능을 느리게하는 요인이 되기 때문이다.
>
> ```java
> 문자열.concat(추가문자열);
> //결합된 문자열 반환
> ```
>
> ```java
> String firstName = "강";
> String lastName = "동원";
> String fullName = firstName.concat(lastName); //강동원 저장
> 
> String firstName = "강";
> String lastName = "호동";
> String fullName = firstName + lastName; //강호동 저장
> ```

### 3.2 contains() 함수

> * contains() 함수는 한 문자열이 특정 문자열을 포함하고 있는지 확인할 때 사용
>
> * 특정 문자열을 포함 여부를 true 또는 false로 반환해준다.
> * 문자열을 검색하는 기능을 추가하고자 할 때 정확한 위치를 알고자 하면 **indexOf()** 함수를, e단순히 포함 여부만을 알고자 하면 **contains()** 함수를 사용하면 좋다.
>
> ```java
> 문자열.contains("찾을 문자열");
> //포함 시 true, 불포함 시 false 반환
> ```
>
> ```java
> String txt = "호기심이 정규교육에서 살아남는 것은 기적이다.";
> System.out.println(txt.contains("기적")); //true 출력
> ```
>
> ```java
> public class StrFun2 {
> 
> 	public static void main(String[] args) {
> 		String greet = "안녕하세요.";
> 		String name = "정우성씨!";
> 		String text = "그들 자신의 눈으로 보고 자신의 심장으로 느끼는 사람들은 극히 드물다.";
> 		System.out.println(greet.concat(name));
> 		System.out.println(text.contains("심장"));
> 		System.out.println(text.contains("정열"));
> 	}
> 
> }
> ```
>
> ![image-20210212220455319](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210212220455319.png)

### 3.3 StringBuffer & StringBuilder 클래스

| String |                StringBuffer                |                StringBuilder                |
| :----: | :----------------------------------------: | :-----------------------------------------: |
|  고정  |               변경이 많을 때               |               변경이 많을 때                |
|        |             성능 ↓ (속도 느림)             |                   성능 ↑                    |
|        | multi thread (thread에 safe, 동기화 처리O) | 단일 thread (thread에 unsafe, 동기화 처리X) |

```java
package stringBuilder;
//StringBuffer, StringBuilder : 긴 문장열을 사용할 때 쓰는 클래스
//@예원
public class UseStringBuilder {
	
	public static void main(String[] args) {
		StringBuilder sb = new StringBuilder(); //StringBuilder 객체 생성
		
		sb.append("Java ");  //문자열을 끝에 추가
		sb.append("Program Study");
		System.out.println(sb.toString());
		
		sb.insert(4, "2"); //index4 위치 뒤에 2를 삽입
		System.out.println(sb.toString());
		
		sb.setCharAt(4, '6'); //index4 위치의 문자를 6으로 변경
		System.out.println(sb.toString());
		
		sb.replace(6, 13, "Book"); //index6 부터 index13 '전'까지를 "Book"문자열로 대치
		System.out.println(sb.toString());
		
		sb.delete(4, 5); //index4 부터 index5 '전'까지 삭제
		System.out.println(sb.toString());
		
		int length = sb.length(); //총 문자 수 얻기
		System.out.println("총 문자 수 : " + length);
		
		String result = sb.toString(); //버퍼에 있는 것을 String 타입으로 리턴
		System.out.println(result);
	}

}
```

![image-20210212224027755](C:\Users\김근묵교수_스마트\AppData\Roaming\Typora\typora-user-images\image-20210212224027755.png)

