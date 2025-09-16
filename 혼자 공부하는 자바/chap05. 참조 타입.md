# 참조 타입
> 자바 타입은 크게 기본 타입(primitive type)과 참조 타입(reference type)으로 분류된다.  
> 기본 타입은 2장에서 다뤘고, 이번 장에선 참조 타입에 대해 알아보자

## 05-1. 참조 타입과 참조 변수
### ▶︎ 기본타입과 참조 타입
`참조 타입(reference type) : 번지를 통해 객체를 참조하는 타입`  

기본 타입과 참조 타입의 차이점은 저장되는 값이다.  
기본 타입은 실제 값을 저장하지만, **참조타입은 메모리의 번지를 변수에 저장**한다.  
종류 : 배열, 열거, 클래스, 인터배이스

#### 📌 메모리에서 변수들이 갖는 값
<img width="1466" height="622" alt="image" src="https://github.com/user-attachments/assets/97955c06-5841-4903-8a6e-18cda5fb6da1" />

### ▶︎ 메모리 사용 영역
자바에서 JVM은 운영체제에서 할당받은 메모리 영역(Runtime Data Area)을 세부 영역으로 구분해서 사용한다.
<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/866cd005-ebf9-4ab2-b98d-5ec4658225a7" />

#### 📌 메소드 영역(Method Area)
JVM이 시작할 때 생성되며, 모든 스레드가 공유하는 영역  
코드에서 사용되는 클래스(~.class)들을 클래스 로더로 읽어 클래스별로 정적필드와 상수, 메소드 코드, 생성자 코드 등을 분류해서 저장

#### 📌 힙 영역(Heap Area)
객체와 배열이 생성되는 영역  

여기에 생성된 객체와 배열은 JVM 스택 영역의 변수나 다른 객체의 필드에서 참조한다.  
**만약 참조하는 변수나 필드가 없다면 JVM이 이것을 쓰레기로 취급하고 쓰레기 수집기(Garbage Collector)를 실행시켜 자동으로 제거**한다.

#### 📌 JVM 스택 영역
메소드를 호출할 때마다 프레임(Frame)을 추가하고 메소드가 종료되면 해당 프레임을 제거하는 동작을 수행  

프레임 내부에는 로컬 변수 스택이 있고, 스택에 기본 타입 변수와 참조 타입 변수가 추가되거나 제거된다.  
스택 영역에 변수가 생성되는 시점 : 변수가 초기화 될 때  
변수는 선언된 블록 안에서만 스택에 존재하고 블록을 벗어나면 스택에서 제거된다.

### ▶︎ 참조 변수의 ==, != 연산
동일한 객체를 참조하는지, 다른 객체를 참조하는지 알아볼 때 사용된다.  

**참조 타입 변수의 값은 힙 영역의 객체 주소이므로 ==, != 연산은 번지 값을 비교하는 것!**
'동일한 번지 값을 갖고 있다' = '동일한 객체를 참조한다'

### ▶︎ null과 NullPointerException
#### 📌 null
null = 참조 타입 변수가 힙 영역의 객체를 참조하지 않는다

null값을 초기값으로 사용할 수 있다.  
따라서 null로 초기화된 참조 변수는 스택 영역에 생성된다.  
참조 타입변수가 null값을 가지는지 확인하려면 ==, != 연산 수행하면 된다.  

#### 📌 NullPointerException
참조 변수를 사용하면서 가장 많이 발생하는 `예외` 중 하나  
참조 변수가 null을 가지고 있을 경우에는, 참조 객체가 없으므로 변수를 통해 객체를 사용할 수 없다.
```java
int[] intArr = null;
intArr[0] = 10;                      // NullPointerException

String str = null;
System.out.println(str.length());    // NullPointerException
```

`예외(Exception) : 프로그램 실행 도중에 발생하는 오류`  

### ▶︎ String 타입
문자열을 저장할 수 있는 참조 변수

문자열 저장 방식
- String변수 우선 선언 후, 문자열 리터럴 대입
- 선언과 동시에 문자열 저장
- `new 연산자`를 이용하여 직접 String 객체 생성하기
  - `new 연산자 : 힙 영역에 새로운 객체를 만들 때 사용하는 연산자, 객체 생성 연산자`
```java
// 1) 변수 선언과 초기화를 동시에
String hobby = "LOL";

// 2) new 이용
String hobby = new String("LOL");
```

일반적으로는 '문자열을 String변수에 저장한다'라고 말하지만, 사실 이는 엄밀히 말해 틀린 표현이다  
문자열이 직접 변수에 저장되는 것이 아니라, String 객체로 생성되고 변수는 String객체를 참조하기 때문  
**String 변수에는 객체의 번지 값이 저장**된다.  

**‼️ 자바는 문자열 리터럴이 동일하다면 String객체를 공유하도록 되어있다.**  
**그러나 문자열 리터럴이 동일하더라도 new를 이용하여 직접 객체를 생성한다면 서로 다른 객체를 참조한다.**

```java
// 1) name1, name2가 동일한 문자열 리터럴 "신용권"을 참조하는 경우, 동일한 String객체를 참조한다
String name1 = "신용권";
String name2 = "신용권";

if( name1 == name2 )       // true
```
<img width="700" height="200" alt="image" src="https://github.com/user-attachments/assets/2c72be18-78cd-4a90-9551-b83ededaf74b" />


```java
// 2) 직접 객체 생성, 서로 다른 String 객체를 참조한다
String name1 = new String("신용권");
String name2 = new String("신용권");

if( name1 == name2 )       // false
```
<img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/a6efea2c-9d41-4586-95b0-779eefdc812d" />

#### 📌 문자열 리터럴을 비교하고 싶을 때, equals() 메소드 
- 원본 문자열과 매개값으로 주어진 비교 문자열이 동일한지 비교한 후 true 또는 false를 리턴한다.
- 원본 문자열.equals(비교 문자열)
```java
String name1 = "신용권";
String name2 = "신용권";
String name3 = "신용";

boolean result = str1.equals(str2);      // true
boolean result = str1.equals(str3);      // false
```
