---
layout: single
title:  "[JAVA_입문_수업] 1장 : 기초개념"
categories: coding
tag: [JAVA_입문_수업]
toc: true
author_profile: true
---

<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 100%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }

    table.dataframe td {
      text-align: center;
      padding: 8px;
    }

    table.dataframe tr:hover {
      background: #b8d1f3; 
    }

    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem Consolas, "Liberation Mono", Menlo, Courier, monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

  .dataframe tbody tr th:only-of-type {
      vertical-align: middle;
  }

  .dataframe tbody tr th {
      vertical-align: top;
  }

  .dataframe thead th {
      text-align: center !important;
      padding: 8px;
  }

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>


# [JAVA_입문_수업] 1장 : 기초개념

해당 게시글은 [JAVA_입문_수업](https://www.youtube.com/playlist?list=PLuHgQVnccGMCeAy-2-llhw3nWoQKUvQck) 을 공부하며 정리한 글입니다.


---


# 변수


- 변수 사용 장점

  - 중복의 제거, 가독성 증가, 유지보수 굿

- 명령어 끝에는 ;를 적어준다.

  - 그렇기 떄문에 int a=1; double b=2; 처럼 한 줄에 두개의 명령어 가능.

- 변수 선언 할 떄는 type을 적어준다.

- 문자는 ''(작은), 문자열은 ""(큰)으로 묶어준다. (여기서 문자는 큰걸 써도 되지만 문자열은 작은거 쓰면x)



```python
int a;
a = 1;
System.out.println(a+1) //2
```



- 정수 : int

- 실수 : double

- 문자열 : String //첫글자 대문자로 작성해야함



```python
# 선언과 동시에 정의 가능
String a = "안녕" 

# 동시 선언 가능
int b,c
b = 1
c = 2
```



주석

- 주석(comment)은 // 으로 사용한다.

- 여러 줄 주석은 /* ~~~~~ */

- JavaDoc주석 : 자바의 문서를 만들 때 사용. /** ~ */ 로 사용한다.



```python
int a = 2
System.out.println(a) //2

/*
System.out.println(a)
System.out.println(a)
*/
```

<br><br><br><br>


---

# 자료형


## 1. 데이터의 크기


- bit : 가장 작은 데이터의 크기

- 8bit = 1byte

- 바이트 단위 끼리는 1024배의 차이가 난다.


<img width="1008" alt="image" src="https://github.com/Jyassmin/Business-Process-Optimization/assets/88031549/20c6889a-a961-4b7c-b539-2d7644b67bb2">



<br><br>


## 2. 종류


- 변수(Varialble) : 변하는 수

- 상수(Constant) : 변하지 않는 값. ex) 1,2,3,..


<img width="658" alt="image" src="https://github.com/Jyassmin/Business-Process-Optimization/assets/88031549/5f0d41d6-5591-44aa-b114-de3fc2a1a1d7">

<img width="552" alt="image" src="https://github.com/Jyassmin/Business-Process-Optimization/assets/88031549/7819bb9b-224e-452f-89d1-b1f29a96538e">


- 문자(char)의 경우, 어느 문자든 2byte.(8bit)

- 마찬가지로 문자열(String)의 경우, 2개의 문자로이루어져 있다면 메모리는 4byte이다.


<br><br>


## 3. 배열(Array)


변수가 하나의 데이터를 저장하기 위한 것이라면,  

배열은 여러 개의 데이터를 저장하기 위한 것이라고 할 수 있다.


### 1) 생성


팀플을 진행하는 하나의 팀의 팀원들의 이름을 그룹화 하고 싶다. 이런 경우 배열을 사용한다.

- `(구성요소의 데이터타입)[] (배열 변수명) = {구성1, 구성2, ...};`

- 아래의 경우 배열에 담길 데이터의 타입이 String이기 때문에 String[]이다.

- 파이썬에서는 [], 대괄호를 사용하지만 여기서는 java가 좋아하는 {}, 중괄호를 쓴다!



```python
String[] classGroup = { "최진혁", "최유빈", "한이람", "이고잉" };
```

메모리 관리를 위해 배열의 크기를 정해놓고 싶다면,  

아래와 같이 크기가 3인 배열 객체를 생성하여 변수에 저장해준다.  

(현실에서도 교실의 크기에는 한계가 있기 때문에, 굳이 책상을 많이 만들어 놓을 필요는 없다.)

> 다만, 이 경우 index가 0~2까지 생성되기에 그 이상의 index생성이 불가능해지며,  

> classGroup[3]을 호출하면 존재하지 않는 인덱스를 사용했기 때문에 오류발생!

- ArrayIndexOutOfBoundsException



```python
String[] classGroup = new String[3];
```

파이썬을 먼저 배운 나로서는 배열의 크기를 먼저 정해서 사용하는 것이 적응이 되지 않는다.  

물론 자바에는 컬렉션 Collection이라는 기능이 있다.  

Container라고도 부르는 이 기능을 이용하면 JavaScript의 배열과 같이 유연하게 배열을 사용할 수 있다.


<br>


### 2) 출력


배열 구성요소의 출력은 (배열명)[`index`]에서 index를 통해 호출한다.



```python
String[] classGroup = { "최진혁", "최유빈", "한이람", "이고잉" };
System.out.println(classGroup[0]);
System.out.println(classGroup[1]);
System.out.println(classGroup[2]);
System.out.println(classGroup[3]);
```

### 3) 삽입


배열의 구성요소는 배열을 선언할 때 넣어줘도 되지만, 선언 이후 추가적으로 삽입을 하려면 출력과 반대의 방법을 사용해야한다.

넣어주고 싶은 위치의 index를 확인 후, 배열[index]를 하나의 변수로 생각하고 값을 대입한다.



```python
public static void main(String[] args) {
    String[] classGroup = new String[4];
    classGroup[0] = "최진혁";
    System.out.println(classGroup.length);
    classGroup[1] = "최유빈";
    System.out.println(classGroup.length);
    classGroup[2] = "한이람";
    System.out.println(classGroup.length);
    classGroup[3] = "이고잉";
    System.out.println(classGroup.length);

}
```

<img width="359" alt="image" src="https://github.com/Jyassmin/Causality_Extraction/assets/88031549/9b6ebe94-6c4c-45fa-a2b6-ee782011c807">


<br><br>


## 4. 참고


> 사용하고자 하는 숫자의 범위에 따라 타입을 유동적으로 선택하며 사용한다!



- 사용되는 메모리의 크기는. 사용된 숫자에 따라 바뀌는 것이 아니라, 선언된 Type에 따라 바뀐다.

- 예를 들어 128이라는 숫자를 사용하고 싶다. 그러면 int a = 128을 사용해야한다. byte는 사용할 수 없음

- 만약, 127을 사용하고 싶다면. int보다는 메모리의 크기가 작은 byte가 더 효율적일 것이다.


<br>


> 정수형의 디폴트는 int, 실수형의 디폴트는 double  

> long정의 할 때는 "L" 명시, float정의 할 때는 "F"  

> int의 경우 큰거 쓸 때 L을 명시하고, double의 경우 작은거 쓸 때 F를 명시하니 반대임에 주의  



- 실수형의 경우 float로 사용해야하는 분명한 이유가 없을 경우. 일반적으로는 double을 사용하도록하자.

  - float타입의 경우 float a = 1.23F; 처럼 뒤에 F를 입력하여 float인 것을 명시해줘야한다.

- 정수형은 기본적으로 int값으로 입력된다. 이말이 무엇이냐

  - long a = 1234124124124141L 처럼 1234124124124141은 int이지만 L을 붙힘으로서 long타입으로 입력할 수 있다.

  - byte, short도 마찬가지로 =120 을 입력할 때 int로 입력되지만, java에서 편의를 위해 뒤에 L같이 명시를 하지 않는다.

  - 그냥 실수형의 디폴트는 double, 정수형의 디폴트는 int라는 것이라는 것을 알고 있어라.


<br><br><br><br>


---

# 형 변환(Type conversion)


같은 숫자라도 타입에 따라 컴퓨터에 저장되는 bit값이 다르다.



- int 200 : 00000000 00000000 00000000 11001000

- float 200F : 01000011 01001000 00000000 00000000


<br><br>


## 1. 자동(암시적) 형변환(Implicit Conversion)

 : 작은 타입에서 큰 타입으로의 변환은 자동으로 바뀔 수 있다.(반대는 x)


<img width="654" alt="image" src="https://github.com/Jyassmin/Business-Process-Optimization/assets/88031549/b1ff530f-7a2f-4003-8103-c73ba6fa1a5b">



```python
ex1) double a = 1.23F # 1.23F는 float이다. 이것이 float보다 더 큰 type인 double에 들어가면 자동으로 형변환이 된다.

ex2) float b = 1.23 # 1.23F는 doulbe. 이것이 dobule 보다 작은 type인 float에 들어가면 오류 발생!!
```


```python
# 더하기 케이스
ex3)
int a = 3;
float b = 1.0F;
double c = a + b;

# int와 float를 합하게 되면.
## 1) int가 flaot로 변하게되고
## 2) a+b에 의해 4.0F가 만들어진다.
## 3) float가 double에 들어가 자동형변환이 일어나며 4.0로 변해, 저장이된다.
```

<br><br>




## 2. 명시적 형변환(Explicit Conversion)

 : 수동적으로 형을 변환한다.


- 자료형의 범위에 주의

- 작은 타입으로 변환할 때 사용하는 것이기 떄문에, 변환 대상이 해당 작은 타입의 최댓값보다 크면 **"정보손실"**이 발생



```python
ex1) float a = (float) 100.0; # 100.0 실수는 기본적으로 double이다. 이를 float로 바꾸려면 상수 앞에 (float)를 명시한다.

ex2) int b = (int)100.0F;

ex3) int c = (int)100.123F; # 이 경우, c는 100이다.(소수점 제외)
```

<br><br><br><br>


---

# 연산자



 : 특정한 작업을 위해 사용되는 기호. 연산자에는 대입, 산술, 비교, 논리연산자 등이 있다.


## 1. 산술연산자

- 산술연산자에는 python에 있는 // 몫 계산 연산자가 없다.<br/><br/>

<img width="304" alt="image" src="https://github.com/Jyassmin/Business-Process-Optimization/assets/88031549/da164398-74a7-4d3d-b224-49833120ac45">


### 1) 다른 타입끼리의 연산.



```python
int a = 10;
int b = 3;
    
float c = 10.0F;
float d = 3.0F;
    
System.out.println(a/b); #3 / int a,b끼리의 연산이기에 소수점을 제외한 3이 출력.
System.out.println(c/d); #3.3333333 / flaot끼리의 연산이기에 소수점 살림.
System.out.println(a/d); #3.3333333 / 자동 형변환 규칙에 따라. int가 float으로 형변환이 되어, float끼리의 연산이 일어남.
```

### 2) 단항 연산자  

<img width="383" alt="image" src="https://github.com/Jyassmin/Business-Process-Optimization/assets/88031549/9519dc1b-db32-4b80-9c57-ba73334d6798">



```python
# ++, --의 경우. 위치에 따라 연산 방식이 달라진다.
int a = 5
System.out.println(i); # 5 출력
System.out.println(++i); # 6 출력 / 5에서 1을 먼저 증가시키고 출력
System.out.println(i++); # 6 출력 / 명령어를 먼저 실행한 뒤 1을 증가시킨다.
System.out.println(i); # 7 출력
```

### 3) 연산 순서(참고)

<img width="647" alt="image" src="https://github.com/Jyassmin/Business-Process-Optimization/assets/88031549/57b3b792-8c75-4a70-8e05-2ab177c40dbd">



<img width="646" alt="image" src="https://github.com/Jyassmin/Business-Process-Optimization/assets/88031549/13683312-250a-4558-98e2-35a412c478d7">



<br><br>


## 2. 비교(관계)연산자

 : 값을 비교할 떄 사용. =, >, >=, =!, == 이 있다.


### 1) ==, .equals() 차이점



- 4번째 줄이 왜 false이냐. 먼저 2번째 줄의 new String을 먼저 알아야함. String처럼 앞의 문자가 대문자이면, 이 자료형은 `참고자료형`이다.<br> 이는 다른 자료형과 저장방법이 다른다. 일반적으로 기본자료형은 stack에 주소값으로 저장되지만, 참고자료형은 실질적으로 heap에 값이 저장되고, 이 주소값이 stack에 다시 저장된다.<br> new String은 새 객체를 생성한다는 뜻이기 때문에 첫번째 줄과 두번째 줄의 "Hello world"는 서로 다른 heap에 저장되며, 이는 다른 객체이다.



- 그렇게 , 4번째 줄의 `==`은 동일한 `객체`인지 알아내는 연산자이고

- 5번째 줄의 `.eqauals()`는 객체들간의 `값`이 같은지 알아내는 연산자이다.



> #### 따라서, 문자간 비교를 할때는 ==이 아닌 .equals()를 사용한다고 알고있자.



```python
String a = "Hello world";
String b = new String("Hello world");

System.out.println(a == b); # flase
System.out.println(a.equals(b)); # true
```

<br><br>


## 3. 논리 연산자

 : 여러 조건 (Boolean)을 결합할 때 사용. 이틀 통해 코드를 간략하게 작성할 수 있다. &&, ||, !이 있다.


어려운 건 없으니, 아래 사진만 참고하도록하자.


![image](https://github.com/Jyassmin/Causality_Extraction/assets/88031549/1cbf70d2-6c96-40df-8e9e-a0c7c34e4caf)



끝!

