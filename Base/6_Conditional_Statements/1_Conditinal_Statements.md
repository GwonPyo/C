<h2> <strong> 1. 조건문 </strong> </h2>

<h3> <strong> (1) if~else if~else </strong> </h3>

우리는 if~else if~else 문을 사용해 프로그램의 흐름을 조정할 수 있다. <br>
아래는 if~else if~else문의 예시 코드다.

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main(void)
{
	int option;
	int num1, num2;
	double result;

	printf("1. 덧셈 2. 뺄셈 3. 곱셈 4. 나눗셈\n");
	printf("옵션 선택: ");
	scanf("%d", &option);
	printf("피연산자 두 개 입력: ");
	scanf("%d %d", &num1, &num2);

	if (option == 1) {
		result = num1 + num2;
	}
	else if (option == 2) {
		result = num1 - num2;
	}
	else if (option == 3) {
		result = num1 * num2;
	}
	else {
		result = (double) num1 / num2;
	}
	printf("결과: %f\n", result);
}
```

<h3> <strong> (2) 삼 항 연산자 </strong> </h3>

삼 항 연산자는 다음과 같은 구조를 가진다.

* (num1>num2) ? (num1) : (num2);

위처럼 삼 항 연산자는 ?, :를 기준으로 나뉜다. (소괄호는 생략가능하다.) <br>
삼 항 연산자는 위의 조건에 만족하면 연산 결과로 num1을 반환하고 거짓이면 num2를 반환한다. <br>
즉, 다음과 같이 변수를 초기화 할 때 사용할 수 있다.

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main(void)
{
	int num1 = 1, num2 = 2;
	int num3 = num1 > num2 ? num1 : num2;
	printf("%d", num3);
}
```