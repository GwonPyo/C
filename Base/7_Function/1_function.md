<h2> <strong> 1. 함수 </strong> </h2>

<h3> <strong> (1) 함수 선언 </strong> </h3>

C언어에서 함수는 다음과 같이 선언한다.

* <b>반환형 함수이름 (반환인자) {...}</b> <br>
Ex) int add(int a, inb b) {...}

위처럼 반환값이 있는 함수는 중괄호 안에 return문을 사용하여 값을 반환해주면 된다. <br>
만약 반환값이 없다면 반환 형태를 void로 설정하고, 매개변수가 없다면 매개변수를 void로 선언하면된다. <br>
단, 반환값이 없어도 함수를 빠져나가고 싶을 때 return문을 사용할 수 있다. <br>

<h3> <strong> (2) 선언과 정의 </strong> </h3>

C언어는 함수의 선언과 정의를 따로 수행할 수 있다. <br>
즉 아래와 같이 먼저 정의 후 선언이 가능하다.

```(c)
#include <stdio.h>

int add(int, int);

int main(void)
{
	int num1 = 1, num2 = 2;
	printf("%d", add(num1, num2));
}

int add(int num1, int num2) {
	return num1 + num2;
}
```

위처럼 정의 부분에서 함수의 매개변수는 아래와 같이 아무렇게나 선언해도 에러가 발생하지 않는다.

* (int, int)
* (int num1, int)
* (int num1, int num2)
