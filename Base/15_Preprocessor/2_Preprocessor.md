<h2> <strong> 2. 선행처리문 </strong> </h2>

<h3> <strong> (1) #define: object-like mecro </strong> </h3>

이전에 봤던 선행처리문을 다시 살펴보자.
* #define PI 3.14

이때 <b>#define을 '지시자', PI를 '매크로', 3.14를 '매크로 몸체'라고 부른다.</b> <br>
#define은 지시자로써 다음과 같은 의미를 지닌다.

* 이어서 등장하는 매크로를 매크로 몸체로 치환해라.

이렇게 #define으로 선언된 매크로를 <b>object-like mecro</b> 혹은 <b>mecro constant</b>라고 부른다.<br>
또한 <b>매크로의 이름은 대문자로 정의</b>하는 것이 일반적이다.

<h3> <strong> (2) #define: Function-like mecro </strong> </h3>

우리는 아래와 같이 <b>함수와 유사한 방식(Function-like mecro)</b>으로도 매크로를 생성할 수 있다.

* #define SQUARE(X) X*X

위와 같은 매크로를 <b>매크로 함수</b>라고도 부른다. <br>
위 선언문은 다음과 같은 의미를 가진다.

* SQUARE(X)라는 패턴이 등장하면 X*X라는 패턴으로 바꿔라.

즉, SQUARE(2)라는 명령문이 등장하면 2*2로 치환된다. <br>
하지만 2+3을 입력하면 2+3*2+3=11과 같은 출력이 발생하니 사용시 주의하도록 하자. <br>
또한 만약 120 / SQUARE(2) -> 120 / 2 * 2로 /가 먼저 계산하게 되니 주의하자. <br> 

> <b> 참고 </b> <br>
위와 같은 문제점은 아래와 같이 괄호를 쳐서 해결 가능하다.
> * 문제1: #define SQUARE(X) (X)*(X)
> * 문제2: #define SQUARE(X) (X*X)

만약 정의하는 <b>메크로의 길이가 길다면 '\'를 활용하여 두 줄에 걸쳐 매크로를 정의</b>해도 된다.

```(c)
#define SQUARE(X) \
((X)*(X))
```

또한 <b>먼저 정의된 매크로는 이후 다른 매크로 정의에 사용 가능</b>하다.