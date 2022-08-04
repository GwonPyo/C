<h2> <strong> 1. while문 </strong> </h2>

while문은 특정조건을 만족하는 동안 해당 블럭의 명령을 반복해서 실행하는 구조다. <br>
예시 코드는 다음과 같다.

```(c)
#include <stdio.h>

int main(void)
{
	int i = 0;
	while (i < 5) {
		printf("반복 횟수: %d\n", ++i); // 1, 2, 3, 4, 5 차례로 출력
	}
}
```

위처럼 while문은 다음과 같은 구조로 사용가능하다.

* while(조건문){ <br>
    &nbsp; &nbsp; &nbsp; 실행문; <br>
    &nbsp; &nbsp; &nbsp; 반복 조건을 무너뜨리기 위한 연산; // Ex) i += 1, i++, ++i <br>
}

추가로 위처럼 while문 중괄호 안의 문장이 한 개라면 중괄호를 다음과 같이 생략할 수 있다.

```(c)
#include <stdio.h>

int main(void)
{
	int i = 0;
	while (i < 5) 
		printf("반복 횟수: %d\n", ++i);
}
```
