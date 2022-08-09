<h2> <strong> 4. 배열과 포인터 </strong> </h2>

<h3> <strong> (1) 배열과 포인터 </strong> </h3>

배열의 이름은 사실 포인터이다. <br>
이때 해당 값은 <b>바꿀 수 없는 상수 형태의 포인터</b>이다 <br>
아래 코드를 살펴보자.

```(c)
#include <stdio.h>

int main(void)
{
	int arr[] = { 1, 2, 3 };
	printf("배열 주소: %p\n", arr);     // arr은 int형 포인터 상수가 된다.
	for (int i = 0; i < sizeof(arr) / sizeof(int); i++)
		printf("%d번째 원소 주소: %p\n", i + 1, &arr[i]);
	 //arr = &arr[1];                  // 컴파일 에러가 발생한다.
}
```

<h3> <strong> (2) 배열 포인터 접근 </strong> </h3>

배열의 이름은 해당 자료형의 포인터 상수이다. <br>
또한 이때 출력되는 주소는 첫 번째 원소의 주소와 동일하다. <br>
따라서 아래와 같이 배열의 이름에 *연산자를 사용하면 첫 번째 원소의 값을 변경할 수 있다.

```(c)
int main(void)
{
	int arr[] = { 1, 2, 3 };
	*arr += 10;
	printf("배열 원소: ");
	for (int i = 0; i < sizeof(arr) / sizeof(int); i++)
		printf("%d ", arr[i]); // 11, 2, 3 출력
}
```

이전에 설명한 것과 같이 위 코드를 보면 배열의 원소들은 인덱싱을 통해 접근 간능하다. <br>
바로 이전에 **배열은 포인터 상수**라고 했다. <br>
즉, 포인터는 인덱싱을 통해 원소들에 접근할 수 있다. <br>
따라서 만약 **포인터 변수가 배열의 주소를 가리키고 있다면 배열과 동일하게 인덱싱을 통해 원소에 접근할 수 있다.**

```(c)
#include <stdio.h>

int main(void)
{
	int arr[] = { 1, 2, 3 };
	int* ptr = arr; // int* ptr = &arr[0];과 동일
	printf("배열 원소: ");
	for (int i = 0; i < sizeof(arr) / sizeof(int); i++)
		printf("%d ", ptr[i]); // 1, 2, 3 출력
}
```

<h3> <strong> (3) 포인터 연산 </strong> </h3>

포인터 변수는 아래와 같이 증감 연산을 수행시킬 수 있다. <br>

```(c)
#include <stdio.h>

int main(void)
{
	int iArr[] = { 1, 2, 3 };
	double dArr[] = { 1.0, 2.0, 3.0 };
	int* iPtr = iArr; double* dPtr = dArr;

	printf("int array 포인터 주소: %p / %d\n", iPtr, iPtr);
	printf("int array 포인터 주소 + 1: %p / %d\n", iPtr + 1, iPtr + 1); // 처음보다 4증가
	printf("int array 포인터 주소 + 2: %p / %d\n", iPtr + 2, iPtr + 2); // 처음보다 8증가

	printf("double array 포인터 주소: %p / %d\n", dPtr, dPtr);
	printf("double array 포인터 주소 + 1: %p / %d\n", dPtr + 1, dPtr + 1); // 처음보다 8증가
	printf("double array 포인터 주소 + 2: %p / %d\n", dPtr + 2, dPtr + 2); // 처음보다 16증가
}
```

위처럼 포인터 변수에 증감 연산을 수행하면 1씩 증가할수록 **해당 포인터 자료형의 byte만큼 증가한다.** <br>
즉, int형 포인터를 n만큼 증가시킨다면 n*4의 크기만큼 주소가 증가된다. <br>

우리는 위와같은 연산을 바탕으로 아래와 같이 배열을 접근할 수 있다.

```(c)
#include <stdio.h>

int main(void)
{
	int iArr[] = { 1, 2, 3 };
	int* iPtr = iArr;
	printf("배열 원소: %d, %d, %d\n", *iPtr, *(iPtr+1), *(iPtr+2)); // 1, 2, 3 출력
}
```

즉, 아래 식들은 모두 동일한 의미를 가진다.

* printf("%d %d %d", ptr[0], ptr[1], ptr[2])
* printf("%d %d %d", *ptr, *(ptr+1), *(ptr+2))
* printf("%d %d %d", arr[0], arr[1], arr[2])
* printf("%d %d %d", *arr, *(arr+1), *(arr+2))

정리하자면 아래 두 식은 같은 의미를 가진다.

* arr[i] == *(arr+i)

<h3> <strong> (4) 포인터 변수로 이루어진 배열 </strong> </h3>

포인터 자료형도 다른 자료형들과 동일하게 배열을 생성할 수 있다. <br>
아래와 같이 기본 생성 방식도 동일하다.

```(c)
#include <stdio.h>

int main(void)
{
	int num1 = 0, num2 = 1, num3 = 2;
	int* arr[] = { &num1, &num2, &num3 };
	printf("%d %d %d", *arr[0], *arr[1], *arr[2]); // 0 1 2 출력
}
```

즉, 우리는 이를 이용해서 **문자열을 저장하는 배열**을 만들 수 있다.

```(c)
#include <stdio.h>

int main(void)
{
	char* arr[] = { "Hi", "C", "Language"};
	printf("%s \n%s \n%s \n", arr[0], arr[1], arr[2]);
}
```