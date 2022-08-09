<h2> <strong> 2. 더블 포인터 </strong> </h2>

<h3> <strong> (1) 이중(더블) 포인터 </strong> </h3>

아래와 같이 * 연산자를 두 개 이어 선언한 포인터를 <b>이중 포인터/더블 포인터</b>라고 부른다. <br>

* int** dptr = &ptr

이전에는 포인터를 다음과 같이 저장했다.

* int num = 0; int* ptr = \&num;

이때 포인터 변수 ptr에는 num의 주소가 저장되는데 이때 우리가 주목해야할 점은 ptr역시 '변수'라는 점이다. <br>
즉, <b>포인터 역시 메모리 공간이 할당되는 변수이므로 &연산자를 사용할 수 있으며 이때 반환되는 주소값을 이중 포인터로 저장할 수 있다. </b>

그리고 이중 포인터를 사용하여 다음과 같은 방식으로 ptr 변수와 num 변수에 접근 가능하다.

* *dptr    // 포인터 변수 ptr에 접근
* *(*dptr) // 변수 num에 접근, **dptr도 가능

아래는 더블 포인터의 예시 코드이다.
```(c)
#include <stdio.h>

int main(void)
{
	int num = 0;
	int* ptr = &num;
	int** dptr = &ptr;

	printf("ptr주소: %9p (ptr) / %9p (*dptr)\n", ptr, *dptr);
	**dptr += 1;
	printf("num: %d\n", num); // 1출력
}
```

<h3> <strong> (2) call by reference </strong> </h3>

두 변수의 값을 바꿔주는 함수는 다음과 같이 선언할 수 있다.

```(c)
#include <stdio.h>

void swap(int* num1, int* num2) {
	int tmp = *num1;
	*num1 = *num2;
	*num2 = tmp;
}

int main(void)
{
	int num1 = 1, num2 = 2;
	printf("%d, %d\n", num1, num2);

	swap(&num1, &num2);
	printf("%d, %d\n", num1, num2);
}
```

만약 두 변수의 값을 바꾸려는게 아니라 두 포인터가 가리키는 곳을 바꾸려면 다음과 같이 구현할 수 있다.

```(c)
#include <stdio.h>

void swap(int** ptr1, int** ptr2) {
	int* tmp = *ptr1;
	*ptr1 = *ptr2;
	*ptr2 = tmp;
}

int main(void)
{
	int num1 = 1, num2 = 2;
	int* ptr1 = &num1, * ptr2 = &num2;
	printf("%d, %d\n", *ptr1, *ptr2);

	swap(&ptr1, &ptr2);
	printf("%d, %d\n", *ptr1, *ptr2);
}
```

<h3> <strong> (3) 포인터형 배열 </strong> </h3>

이전에 아래와 같이 포인터형 배열을 선언하는 방법을 배웠다.

* int* arr[10];

이때 배열이름 arr은 배열의 첫 번째 원소, int 형 포인터의 주소를 가리킨다. <br>
즉, arr은 더블 포인터인 것이다. <br>
아래 코드를 살펴보면 arr이 더블 포인터인 것을 확인할 수 있다.

```(c)
#include <stdio.h>

int main(void)
{
	int num1 = 1, num2 = 2, num3 = 3;
	int* arr[] = { &num1, &num2, &num3 };
	int** dptr = arr;

	printf("%d, %d, %d\n", *arr[0], *arr[1], *arr[2]);
	printf("%d, %d, %d\n", *dptr[0], *dptr[1], *dptr[2]);
}
```