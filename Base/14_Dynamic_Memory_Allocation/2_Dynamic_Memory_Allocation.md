<h2> <strong> 2. 메모리 동적 할당 </strong> </h2>

우리는 지역변수처럼 함수 호출마다 할당이 이뤄지고, 전역변수와 같이 함수 종료시 소멸되지 않는 특징을 가진 변수가 필요할 때가 있다. <br>
예를 들어, 임의의 함수가 있다고 가정하고 아래 상황을 살펴보자.

1. 함수 안에 문자열 지역변수(배열)를 선언한다.
2. 표준 입력 스트림으로부터 문자열을 받아와서 해당 배열에 저장한다.
3. 해당 배열의 포인터를 main 문의 문자열 포인터에 전달한다.

위 경우 함수 안에 있는 문자열 배열이 지역변수기 때문에 함수 종료시 소멸되고 이후에 문제가 발생할 수 있다. <br>
이번엔 다른 경우를 살펴보자.

1. 전역 변수로 문자열 배열을 선언한다.
2. 이전과 같이 함수 안에서 해당 전역 변수를 초기화한다.
3. 해당 배열이 포인터를 반환해 main 문의 문자열 포인터1에 전달한다.
4. 동일한 과정을 똑같이 반복해 main 문의 문자열 포인터2에 전달한다.

이 경우 이전에 초기화한 문자열 포인터1의 내용이 사라지고 포인터2의 값과 동일해져 버린다. (둘다 전역변수의 주소를 가리키기 때문이다.)

즉 우리는 위에서 말했듯, 지역변수이자 전역변수의 특징을 가지는 변수를 필요로 한다. <br>

<h3> <strong> (1) malloc & free </strong> </h3>

malloc 함수는 메모리 공간을 할당하고 free 함수는 할당된 메모리 공간을 해제하는 함수다. <br>
둘의 구조는 다음과 같다.

* #include <stdlib.h>
* <b>void* malloc(size_t size);</b>
* <b>void free(void* ptr);</b>

malloc 함수는 할당 성공시 할당된 메모리 주소의 값을 반환하고 실패시 NULL을 반환한다. <br>
우리는 반환된 void형 포인터를 형 변환하여 아래와 같이 사용 가능하다.

```(c)
#include <stdio.h>
#include <stdlib.h>

int main(void)
{	
	int* ptr1 = (int*)malloc(sizeof(int));
	int* ptr2 = (int*)malloc(sizeof(int)*10);

	*ptr1 = 10;
	for (int i = 0; i < 10; i++) {
		*(ptr2 + i) = *ptr1 * i;
	}

	for (int i = 0; i < 10; i++)
		printf("%d ", *(ptr2 + i));

	free(ptr1);
	free(ptr2);
}
```

위와 같이 malloc 함수를 사용하여 메모리 공간을 할당하는 것을 <b>동적 할당(Dynamic allocation)</b>이라고 한다. <br>

<h3> <strong> (2) calloc </strong> </h3>

calloc 역시 malloc처럼 힙 영역에 메모리 공간을 할당할 수 있다. <br>
단, malloc과 인자 전달 방식이 다르다.

* <b>void* calloc(size_t elt_count, size_t elt_size);</b>

calloc 역시 할당 성공시 메모리 주소를 반환하며 실패시 NULL을 반환한다. <br>
단, malloc과 다르게 2개의 인자를 전달받는다. <br>
둘의 차이는 다음과 같다.

* malloc(100): 100 바이트를 힙 영역에 할당.
* calloc(4, 25): 4바이트 크기의 블록 25개를 힙 영역에 할당.

또한 <b>malloc의 경우 할당된 메모리 공간에 쓰레기 값으로 채워지지만 calloc은 모든 비트를 0으로 초기화한다.</b>

<h3> <strong> (3) realloc </strong> </h3>

임의의 배열의 크기를 늘리는 것은 불가능하다. <br>
하지만 힙 영역에서는 이러한 작업이 가능하다.

* <b>void* realloc(void* ptr, size_t size);</b>

위 수식의 의미는 다음과 같다.

* ptr이 가리키는 메모리의 크기를 size 크기로 조절해라.

realloc 함수는 성공시 새로 할당된 메모리의 주소 값을 반환하고, 실패시 NULL을 반환한다. <br>
이때 반환된 주소는 이전 주소와 같을 수도 있고 다를 수도 있으며 해당 포인터 배열에 담겨있던 값들은 복사되어 옮겨진다. <br>
아래는 calloc과 realloc 사용 예시 코드다.

```(c)
#include <stdio.h>
#include <stdlib.h>

int main(void)
{	
	int* ptr1 = (int*)calloc(sizeof(int), 5);

	for (int i = 0; i < 5; i++) {
		*(ptr1 + i) = i * 10;
	}

	int* ptr2 = (int*)realloc(ptr1, 20);

	for (int i = 5; i < 10; i++) {
		*(ptr2 + i) = i * 10;
	}

	for (int i = 0; i < 10; i++)
		printf("%d ", *(ptr2 + i));

	printf("%p %p", ptr1, ptr2);

	free(ptr1);
	free(ptr2);
}
```