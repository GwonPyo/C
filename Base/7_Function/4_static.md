<h2> <strong> 4. static </strong> </h2>

static을 지역변수 앞에 사용하면 다음과 같은 특징을 가진다.

1. 해당 함수 내에서만 접근할 수 있다.
2. 프로그램 종료까지 메모리 공간에 존재한다.

즉, 지역변수와 전역변수의 특징이 공존하며 '해당 함수(지역)내에서만 사용 가능한 전역변수'라고 생각할 수 있다. <br>

다음은 static 예시 코드이다.

```(c)
#include <stdio.h>

int example();

int main(void)
{
	for (int i = 0; i < 3; i++) {
		example();
	}
	// printf("local_num: %d", static_num); // static_num 접근 불가
}

int example() {
	static int static_num = 0;
	int local_num = 0;
	static_num++; local_num++;
	printf("static_num: %d, local_num: %d\n", static_num, local_num); // 결과: 1, 1 / 2, 1 / 3, 1
}
```