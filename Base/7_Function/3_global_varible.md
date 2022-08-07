<h2> <strong> 3. 전역변수 </strong> </h2>

전역변수는 지역변수와 반대로 모든 곳에서 접근할 수 있는 변수다. <br>
다음은 전역변수 예시 코드다.

```(c)
#include <stdio.h>

int example();
int global_num = 20;

int main(void)
{
	global_num += 1;
	printf("main num: %d\n", global_num);
	example();
}

int example() {
	global_num += 1;
	printf("example num: %d\n", global_num);
}
```

전역변수는 다음과 같은 특징을 가진다. <br>

* 초기화하지 않으면 0으로 초기화된다.
* 프로그램 전체 영역에서 접근 가능하다.
* 동일한 이름의 지역변수 선언시 지역변수가 전역변수를 가린다.
