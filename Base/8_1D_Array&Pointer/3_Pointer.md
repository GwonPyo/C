<h2> <strong> 3. 포인터 </strong> </h2>

<h3> <strong> (1) 포인터 선언 </strong> </h3>

포인터 변수는 메모리 주소 값을 저장하기 위한 변수로 다음과 같이 선언이 가능하다.

```(c)
#include <stdio.h>

int main(void)
{
	int num = 0;
	int* pointer = &num;
	printf("%p", pointer); // 000000B629D3F614 출력
}
```

위처럼 &연산자를 사용하면 해당 변수의 주소값을 가져올 수 있다. <br>
지금까지 우리가 scanf에 사용했던 &역시 이 주소값을 받아오기 위함이다. <br>
참고로 아래 식들은 모두 같은 의미를 가진다.

* int* ptr;
* int *ptr;
* int * ptr;

추가적으로 포인터는 선언 이후에 유효한 주소값을 채워 넣을 것이라면 **NULL 포인터**를 사용하는 것이 좋다. <br>
NULL 포인터는 다음과 같이 선언가능하다.

* int* ptr = NULL; 
* int* ptr = 0;

위와 같이 NULL 포이터를 사용하면 해당 포인터는 아무곳도 가리키지 않게 된다. <br>
즉, 메모리의 잘못된 접근을 미연에 방지할 수 있음으로 기억하도록하자.

<h3> <strong> (2) * 연산자 </strong> </h3>

포인터 변수에 *연산자를 붙이면 해당 주소에 할당된 변수가 가진 값에 접근이 가능하다. <br>
아래는 *연산자로 포인터가 가리키는 변수의 값에 접근해본 코드이다.

```(c)
#include <stdio.h>

int main(void)
{
	int num1 = 100, num2 = 100;
	int* pnum1 = &num1, * pnum2 = &num2;
	*pnum1 += 30;
	*pnum2 -= 30;

	printf("num1: %d / num2: %d\n", *pnum1, *pnum2); // 130, 70 출력
}
```