[TOC]

# C#

---

## 1. 참고사이트

[프로그래머스 c#](https://school.programmers.co.kr/learn/courses/1/1-unity%EB%A1%9C-%EB%B0%B0%EC%9A%B0%EB%8A%94-c)

##  2. 리터럴

프로그래밍에서 상수 값을 나타내는 표기법. 변수나 식별자를 통해 계산되거나 참조되지 않는다.

> C# 컴파일러는 `int, double, char, string, bool` 데이터 타입에 그 값을 할당한다.

```c#
123  // int 리털
12.3 // double 리터럴
"A"  // string 리터럴
"a"  // char 리터럴
true // bool 리터럴
```

- **float** 데이터 타입은 숫자 뒤에 `123.45F`와 같이 F를 붙여 double이 아닌 float 타입임을 나타냄.
- **double** 데이터 타입은 숫자 뒤에 123.45D와 같이 D를 붙이거나 혹은 아무것도 붙이지 않음으로 double 타입임을 나타냄.
- **decimal** 데이터 타입은 숫자 뒤에 123.45M과 같이 M을 붙여 decimal 타입임을 나타냄.
- **char** 데이터 타입은 작은따옴표 ' (single quotation)을 사용하여 한 문자를 할당.
- **string** 데이터 타입은 큰따옴표 " (double quotation)을 사용하여 문자열을 할당.



## 3. 배열

배열은 **레퍼런스(Reference)** 타입이기 때문에, 배열을 다른 객체나 메서드에 전달할 때, 직접 모든 배열 데이터를 복사하지 않고, 배열 전체를 가리키는 참조 값(Reference pointer)만을 전달한다. 즉, 전달하는 쪽에서는 단순히 레퍼런스인 배열명을 사용하며, 받는 쪽에서는 배열 데이터 타입 및 배열 파라미터명을 사용.

```c#
// 1차 배열
string[] players = new string[10];
string[] regions = { "서울", "경기", "강원" };

// 2차 배열
string[,] depts = {{"김과장", "인사팀"},{"이대리", "총무팀"}}

// 3차 배열
string[,,] cubes;

//-------------------------------------------
// Jagged Array 가변배열
// 1차 배열 크기(3) 명시 
int[][] A = new int[3][];

// 각 1차 배열 요소당 서로 다른 크기 배열 할당
A[0] = new int[2];
A[1] = new int[3] {1, 2, 3};
A[2] = new int[4] {1, 2, 3, 4};

A[0][0] = 1;
A[0][1] = 2;

```

