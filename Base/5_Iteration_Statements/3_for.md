<h2> <strong> 3. for문 </strong> </h2>

for문은 가장 많이 사용되는 반복문으로 반복을 위한 <b>변수 선언, 반복 조건을 무너뜨리기 위한 연산을 묶을 수 있는 반복문</b>이다. <br>
for문은 다음과 같은 구조를 가진다.

* for(초기식; 조건식; 증감식){ <br>
    &nbsp; &nbsp; &nbsp; 실행문; <br>
}

이전에 작성한 while문 코드를 for문 코드로 바꾸면 다음과 같다.

```(c)
int main(void)
{
	int num1 = 0;
	for (num1; num1 < 5; ++num1) {
		printf("반복 횟수: %d\n", num1); // 0, 1, 2, 3, 4 출력
	}
	for (int num2 = 0; num2 < 5; num2++) {
		printf("반복 횟수: %d\n", num2); // 0, 1, 2, 3, 4 출력
	}
}
```

for문은 아래와 같이 초기식, 조건식, 증감식 등을 생략하고 사용할 수 있다.

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main(void)
{
	int num = 0;
	int result = 0;

	for (; num >= 0;) {
		result += num;
		printf("더할 정수를 입력하세요(음수 입력시 종료): ");
		scanf("%d", &num);
	}
	printf("결과: %d", result);
}
```

만약 위처럼 쵝식, 증감식이 아니라 조건식이 생략된 경우 무한루프가 발생하니 주의하자.
하지만 가급적이면 초기식, 증감식 위치에 반복 조건과 관련된 연산식을 넣어두는 것이 좋다. <br>
