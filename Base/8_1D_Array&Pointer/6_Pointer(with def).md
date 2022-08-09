<h2> <strong> 6. 포인터와 함수 </strong> </h2>

<h3> <strong> (1) 함수의 매개변수 </strong> </h3>

이전에 함수 선언에서 배웠던 것과 같이 함수는 다음과 같이 선언한다. 

* [자료형] [함수이름] (매개변수1, 매개변수2, ...)

이때 매개변수는 <b>전달된 변수의 값을 복사한다.</b> <br>
즉, 전달된 변수와 함수의 매개변수는 서로 별개의 변수가 된다. <br>
따라서 매개변수의 값을 변경해도 실제 전달됐던 변수에는 영향을 미치지 않는다.<br>

<h3> <strong> (2) 매개변수로 배열 전달 </strong> </h3>

함수의 매개변수로 배열을 받으려면 배열을 선언할 수 있어야 하지만 이것은 허용되지 않는다. <br>
따라서 우리는 <b>배열의 주소를 사용해 배열을 인자로 전달해야 한다.</b>
즉, 함수는 다음과 같이 선언하면 배열을 인자로 받을 수 있다.

* <b>void example(int* arr){...}</b>

다음은 매개변수로 배열을 전달하는 코드 예시이다.

```(c)
#include <stdio.h>

void example(int*);

int main(void)
{
	int arr[] = { 1, 2, 3, 4, 5 };
	int len = sizeof(arr) / sizeof(int);
	
	printf("변경전 원소: ");
	for (int i = 0; i < len; i++)
		printf("%d ", arr[i]); // 1 2 3 4 5 출력
	printf("\n");

	example(arr, len);
	printf("변경후 원소: ");
	for (int i = 0; i < len; i++)
		printf("%d ", arr[i]); // 11 22 33 44 55 출력
}

void example(int* arr, int len) {
	for (int i = 0; i < len; i++)
		arr[i] += (i+1)*10;
}
```

위에서 배열의 길이 len을 전달한 이유는 해당 배열의 길이를 함수내에서 계싼할 수 없기 때문이다. <br>
<b>함수 내에서는 전달된 배열의 길이를 계산할 수 없다는 사실을 꼭 기억하자.</b>

또한 배열을 인자로 받을 때 다음과 같이 전달받을 수도 있다. <br>
아래 방식이 배열을 인자로 받는다는 느낌을 확실히 주므로 주로 아래 형태를 많이 사용한다고 한다. <br>

* <b>void example(int arr[])</b>

<h3> <strong> (3) Call by Value/Reference </strong> </h3>

Call by Value 방식은 함수에 값을 전달하는 방식으로 우리가 포인터를 배우기 이전에 사용했던 방식이다. <br>
Call by Reference 방식은 위에서 사용한 것처럼 주소값을 넘겨주고, 우리가 해당 <b>매개변수로 전달된 변수에 직접 접근이 가능한 방식이다.</b> <br>
예를 들어 아래와 같은 접근이 가능하다.

```(c)
#include <stdio.h>

void example(int*, double*);

int main(void)
{
	int num1 = 10; double num2 = 20.0;
	printf("변경전: %d %.2f\n", num1, num2); // 10 20.00

	example(&num1, &num2);
	printf("변경후: %d %.2f\n", num1, num2); // 11 22.00
}

void example(int* num1, double* num2) {
	*num1 += 1;
	*num2 += 2;
}
```

<h3> <strong> (4) const </strong> </h3>

포인터는 다음과 같이 두 가지 상수 선언 방식이 있다.

* <b>const</b> int* ptr
* int* <b>const</b> ptr

위에서 첫 번째 방식을 사용하면 해당 포인터의 주소값을 변경할 수는 있지만, 해당 주소에 저장된 값을 변경할 수는 없다. <br>
두 번째 방식은 해당 주소에 저장된 값은 변경할 수 있지만, 포인터가 가리키는 주소는 변경할 수 없다.