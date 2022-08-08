<h2> <strong> 3. 포인터와 문자열 </strong> </h2>

이전에 우리는 문자열을 다음과 같이 선언했다.

* char str[] = "Hi C Language";

추가적으로 문자열 선언시 char형 포인터를 이용하면 다음과 같이 선언할 수 있다.

* char * str = "Hi C Language";

위와 같이 문자열을 선언하면 메모리 공간에 문자열이 저장되고, 문자열의 첫 번째 문자의 주소값이 반환된다. <br>
즉, 첫 번째 문자의 주소값이 포인터 변수에 저장된다. <br>

위 두 개의 선언문은 다음과 같은 차이를 가진다.

|종류|배열 선언|포인터 선언|
|:---:|:---:|:---:|
|문자열 내 문자 변경|가능|불가능|
|문자열 자체 변경|불가능|가능|

위와 같은 특성 때문에 우리는 배열로 문자열을 선언하면 **변수 형태의 문자열**, 포인터로 선언하면 **상수 형태의 문자열**이라고 부른다. <br>

```(c)
#include <stdio.h>

int main(void)
{
	char str1[] = "arr string";
	char* str2 = "ptr string";

	printf("Array\n");
	printf("수정 전: %s\n", str1); // arr string
	str1[0] = 'A';
	printf("수정 후: %s\n", str1); // Arr string
	 
	printf("\n");
	printf("Pointer\n");
	printf("수정 전: %s\n", str2); // ptr string
	// str2[0] = 'P';			  // 해당 코드 실행시 아래 코드 실행 x
	str2 = "Ptr string";
	printf("수정 후: %s\n", str2); // Ptr string
}
```