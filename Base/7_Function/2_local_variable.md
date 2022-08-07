<h2> <strong> 2. 지역변수 </strong> </h2>

C언어에서는 중괄호 안에 선언된 모든 변수는 지역변수가 된다. <br>
다음 코드를 보면 main함수와 example함수의 num이 다르게 출력되는 것을 확인할 수 있다.

```(c)
#include <stdio.h>

int example();

int main(void)
{
	int num = 0;
	printf("main num: %d\n", num);      // 0
	example();
}

int example() {
	int num = 10;
	printf("example num: %d\n", num);   // 10
}
```

지역변수는 다음과 같은 특징을 가진다.

* 선언된 지역 내에서만 유효하다.
* 다른 함수와 이름이 겹쳐도 문제되지 않는다.

<h3> <strong> (1) 내부 동작 </strong> </h3>

지역변수는 메모리의 stack이라는 부분에 쌓이는데 이전 코드의 동작 과정은 다음과 같다. <br>

1. main의 num이 stack에 할당된다.
2. example의 num이 stack에 할당된다.
3. example함수 종료 후 example의 num은 메모리 공간에서 소멸된다.
4. main의 num이 메모리 공간에서 소멸된다.