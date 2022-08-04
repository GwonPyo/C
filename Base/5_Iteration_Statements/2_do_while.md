<h2> <strong> 2. do~while문 </strong> </h2>

이전에 while문은 다음과 같은 형태로 진행됐다.

1. 조건문을 검사한다.
2. 조건문이 참이라면 반복문 안의 내용을 실행한다.
3. 위 과정을 반복한다.

do~while문은 while문과 같은 반복문이지만 조건문의 검사 시점에서 차이가 있다. <br>
다음은 do~while문과 while을 비교한 예시코드이다.

```(c)
#include <stdio.h>

int main(void)
{
	int i = 0;
	do {
		printf("반복 횟수: %d\n", ++i); // 1 출력
	} while (i < 0);

	i = 0;
	while (i < 0) {
		printf("반복 횟수: %d\n", ++i); // 아무것도 출력하지 않음.
	}
}
```

위처럼 while문은 조건문에 만족하지 않으면 한 번도 실행되지 않는다. <br>
하지만 do~while문은 <b>무조건 한 번 실행 후 조건을 검사</b>하므로 최소한 한 번은 실행되는 구조를 가진다.