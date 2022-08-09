<h2> <strong> 1. 함수 포인터와 void 포인터 </strong> </h2>

<h3> <strong> (1) 함수 포인터 </strong> </h3>

함수 역시 메모리에 저장되기 때문에 함수도 주소 값을 가진다 <br>
이 주소 값을 저장하는 것이 <b>함수 포인터 변수</b>다.
<b>즉, 배열과 동일하게 함수의 이름은 함수가 저장된 메모리 공간의 주소 값을 의미하며 상수이다.</b> <br>

함수의 주소를 저장하기 위한 포인터 형은 <b>반환형과 매개변수의 선언</b>을 통해 결정짓는다. <br>
즉, int example(int num1, int num2)라고 하면 <b>반환형이 int이고 두 개의 int형 변수를 매개변수로 받는 포인터 형</b>을 선언해야 한다.<br>
이때 위 함수는 다음과 같은 포인터 형으로 표현한다. <br>

* <b> int (*ptr) (int, int) = example -> 반환형이 int이고 두 개의 int형 매개변수를 받는 함수의 포인터 형 </b>

위처럼 함수 포인터 변수를 선언하면 ptr(num1, num2)로 함수를 호출할 수 있다.

<h3> <strong> (2) void 포인터 </strong> </h3>

void 포인터는 어떠한 형태(변수, 배열, 함수 등)의 주소도 저장이 가능하지만 아무런 포인터 연산도 불가능하다는 특성을 가진다.<br>
void 포인터는 다음과 같이 선언한다.

* <b>void* ptr</b>

void 포인터는 <b>주소 값에만 의미를 두고, 포인터 형은 나중에 결정</b>할 때 유용하다고 한다.

<h3> <strong> (3) main 함수 </strong> </h3>

지금까지 우리는 다음과 같은 형태의 main 함수를 정의했다.

* int main(void) {}

하지만 main 함수는 아래 방식으로도 저장 가능하다.

* int main(int argc, char * argv[]) {}

프로그램 실행 시 main 함수로 전달할 인자를 결정할 수 있고, main 함수도 이러한 인자들을 전달받을 수 있도록 제한된 형태의 매개변수 선언이 가능하다. <br>

먼저 아래 소스코드를 살펴보자.

```(c)
#include <stdio.h>

int main(int argc, char* argv[])
{
	printf("전달된 문자열 개수: %d\n", argc);

	for (int i = 0; i < argc; i++)
		printf("%d번째 문자열: %s\n", i+1, argv[i]);
}
```

해당 소스코드를 컴파일 시키고 나온 exe파일(main_func.exe)을 cmd로 실행시켜보면 다음과 같은 결과가 나온다.

![image](https://user-images.githubusercontent.com/85156021/183777790-51fcce56-c7bb-4b1d-8e47-127f0a46cf32.png)

main_func는 main_func.exe 파일을 실행하라는 명령이고, 해당 <b>exe파일 실행시 전달된 문자열 개수와, 문자열 배열이 전달된다.</b> <br>
단, 이때 ""를 사용하면 문자열을 묶을 수 있다. <br>
예를 들어, main_func "Hi Main Function"이라고 입력하면 문자열 2로 입력된다.

