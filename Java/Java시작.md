# JAVA 특징

---

[TCP스쿨](https://www.tcpschool.com/java/java_intro_basic)

`장점`

1. 자바는 운영체제와는 독립적으로 실행 가능
2. 불필요한 기능을 과감히 제거하여 다른 언어에 비해 습득이 쉬운편
3. 자동 메모리 관리 등을 지원하여 다른 언어에 비해 안정성이 높다
4. 연산자 오버로딩을 금지하고 제네릭을 도입함으로써 코드의 가독성을 높힘
5. 커뮤니티에 정보가 다양하다

`단점`

1. 실행을 위해 자바 가상 머신을 거쳐야 하므로, 다른 언어에 비해 실행 속도가 느리다
2. 예외 처리가 잘 되어 있지만, 개발자가 일일이 처리를 지정해 줘야한다
3. 다른 언어에 비해 작성해야 하는 코드가 긴 편이다



## System.out.println()

---

System 클래스에는 표준 입출력을 위해 다음과 같은 클래스 변수가 정의되어 있다

1. System.in
2. System.out
3. System.err

자바에서는 System.in 스티름을 사용하여 표준 입력 작업을 수행한다.

또한, System.out 스트림이나 System.err 스트림을 사용하여 표준 출력 작업을 수행

```java
System.out.print("출력할데이터");	  // 결과 후 줄바꿈
System.out.println("출력할데이터"); // 결과 후 줄바꿈x
```



## SE8

---

### 람다표현식

```java
// 기존 방식
new Thread(new Runnable(){
    public void run(){
        System.out.println("전통적인 방식의 일회용 스레드 생성");
    }
}).start();

// 람다 표현식
new Thread(()->{
    System.out.println("람다 표현식을 사용한 일회용 스레드 생성");
}).start()
```



### 스트림API

```java
String[] arr = new String[]{"넷", "둘", "셋", "하나"};

// 배열에서 스트림 생성
Stream<String> stream1 = Arrays.stream(arr);
stream1.forEach(e -> System.out.print(e + "e"));
System.out.println();

// 배열의 특정 부분만을 이용한 스트림 생성
Stream<String> stream2 = Arrays.stream(arr, 1, 3);
stream2.forEach(e -> System.out.print(e + " "));

// 실행결과
// 넷 둘 셋 하나
// 둘 셋
```



### java.time

JDK 1.0에서는 Date 클래스를 사용하여 날짜에 관한 처리를 수행하였지만 현재 대부분의 메소드가 사용을 권장하지 않고 있다(deprecated)

JDK 1.1부터 새롭게 제공된 Calendar 클래스는 날짜와 시간에 대한 정보를 얻을 수 있지만, 다음과 같은 문제점이 존재

1. Calendar 인스턴스는 불변 객체(immutable object)가 아니라서 값이 수정될 수 있습니다
2. 윤초(leap second)와 같은 특별한 상황을 고려하지 않음
3. Calendar 클래스에서는 월을 나타낼 때 1월부터 12월을 0부터 11로 표현해야함

그리하여 Java SE 8 버전에서는 Calendar 클래스보다 더 나은 성능의 `Joda-Time`라이브러리를 발전시킨 날짜와 시간 API인 java.time 패키지를 제공

```java 
LocalDate today = LocalDate.now();
System.out.println("올해는 " + today.getYear() + "년입니다.");

LocalDate otherDay = today.withYear(1982);
System.out.println("올해는 " + otherDay.getYear() + "년입니다.");

// 실행결과
// 올해는 2017년 입니다.
// 올해는 1982년 입니다.
```

