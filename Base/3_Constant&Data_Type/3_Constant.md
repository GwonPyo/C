<h2> <strong> 3. 상수 </strong> </h2>

상수는 <b>변경이 불가능한 데이터</b>를 말하며 변수의 상대적 개념이다. <br> 
크게 <b>이름이 있는 상수</b>와 <b>이름이 없는 상수</b>로 나뉜다.

<h3> <strong> (1) 이름이 없는 상수 </strong> </h3>

우리는 임의의 수로 연산된 데이터를 변수에 다음과 같이 저장한 적이 있다.

* int num = 1 + 2;

위 코드는 다음과 같은 방식으로 작동된다.

1. 1+2의 연산을 하기 위해 <b>1과 2를 메모리 공간에 상수 형태로 저장한다.</b>
2. 두 상수로 덧셈 연산을 진행한다.
3. 덧셈의 결과를 변수 num에 저장한다.

위 과정에서 중요한 점은 1과 2는 num과 달리 저장된 메모리 공간의 이름이 없다. <br>
이와 같이 이름이 없는 상수를 <b>리터럴(literal)</b>이라고 부른다. 

<h3> <strong> (2) 리터럴의 자료형 </strong> </h3>

리터럴에도 자료형이 존재한다. <br>
임의의 리터럴에 대한 자료형은 다음과 같다.

* 정수: int 
* 실수: double
* 문자: char

리터럴의 자료형을 확인해 보고 싶다면 아래와 같이 sizeof 함수를 사용할 수 있다.

```(c)
#include <stdio.h>

int main(void)
{
	printf("정수형: %d\n", sizeof(1));		// 4
	printf("실수형: %d\n", sizeof(1.0));	// 8
	printf("문자형: %d\n", sizeof('A'));	// 4
}
```

만약 해당하는 자료형과 다른 자료형을 사용하고 싶다면 <b>접미사</b>를 통해 다음과 같이 변경할 수 있다.

```(c)
#include <stdio.h>

int main(void)
{
	printf("정수형: %d\n", sizeof(1LL));	// 8
	printf("실수형: %d\n", sizeof(1.0F));	// 4
}
```

위 코드에서 1은 접미사 LL로 인해 long long이 되고, 1.0은 F로 인해 float이 된다. <br>
C언어에는 다음과 같은 접미사가 존재한다.

|종류|접미사|자료형|
|:---:|:---:|:---:|
|정수형|U <br> L <br> UL <br> LL <br> ULL|unsigned int <br> long <br> unsigned long <br> long long <br> unsigned long long|
|실수형|F <br> L|float <br> long double|

위 접미사는 모두 <b>대소문자를 구분하지 않는다.</b>

<h3> <strong> (3) 이름이 있는 상수 </strong> </h3>

이름이 있는 상수는 <b> 심볼릭(Symbolic) 상수 </b>라고 부르며 <b> const 키워드 </b>를 사용해 표현할 수 있다. <br>
const를 사용해 상수를 선언하는 방법은 다음과 같다. <br>

* const int PI = 3.14;

상수는 선언 이후에 값을 변경할 수 없기 때문에 위처럼 선언과 동시에 선언해야한다. <br>
또한 <b>관례적으로 상수의 이름은 모두 대문자로 표시하며 둘 이상의 단어를 연결할 때는 언더바(_)를 사용한다.</b>

