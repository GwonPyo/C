<h2> <strong> 3. 문자열 관련 함수 </strong> </h2>

<h3> <strong> (1) 문자열 입출력 함수 </strong> </h3>

지금까지 문자열을 출력하기 위해서 printf와 scanf 등의 함수를 사용했다. <br>
먼저 문자열 출력에 사용하는 함수를 알아보자.

* <b>int puts(const char * s);</b>
* <b>int fputs(const char * s, FILE * stream);</b>

puts는 출력 대상이 표준 출력 스트림이지만 fputs는 출력 대상 스트림을 변경할 수 있다. <br>
단, puts 함수는 호출시 문자열 출력 후 자동으로 개행이 수행되고, fputs 함수는 그렇지 않다. <br>

이전에 scanf의 경우 "hi c"와 같이 공백이 있는 문자열을 입력받을 때 "hi"밖에 입력받지 못했다. 아래 함수는 이러한 문자열도 입력받을 수 있다.

* <b>char* gets(char* s);</b>
* <b>char* fgets(char* s, int n, FILE* Stream);</b>

gets 함수는 문자열을 입력받아 배열에 넣어준다. <br> 
하지만 배열의 길이보다 입력 받은 문자열의 길이가 긴 경우 에러가 발생한다. <br>
따라서 fgets를 사용하여 문자열을 배열의 길이만큼 저장할 수 있도록 설정하는 것이 좋다.<br>

아래는 fgets를 통해 문자열을 입력받는 예시 코드다.

```(c)
#include <stdio.h>

int main(void)
{
	char str[7];

	for (int i = 0; i < 3; i++) {
		fgets(str, sizeof(str), stdin);
		printf("%d번째 문자열: %s\n", i + 1, str);
	}
}
```

> <b>(참고)</b>
> 1. 문자열 입력시 배열의 길이에 맞게 null 문자도 포함되어 입력된다.
> 2. 문자열 입력시 개행 문자(\n)도 입력에 포함된다.

<h3> <strong> (2) 길이 반환 함수 (strlen) </strong> </h3>

아래 함수를 사용하면 문자열의 길이를 반환해준다. <br>

* <b>size_t strlen(const char* s);</b>

size_t의 반환형은 일반적으로 아래와 같이 선언되어 있다. <br>

* typedef unsigned int size_t;

위 코드는 <b>'unsigned int의 선언을 size_t로 대신할 수 있다.'</b>를 의미한다.<br>
즉, 아래 두 식은 동일하다.

* size_t size;
* unsigned int size;

아래는 해당 함수를 사용한 예시다.

```(c)
#include <stdio.h>
#include <string.h>

void RemoveBSN(char* str) {
	int len = strlen(str);
	str[len - 1] = 0;		// 마지막 개행 문자를 0(null 문자)으로 바꿈
}

int main(void)
{
	char str[50];

	printf("문자열 입력: ");
	fgets(str, sizeof(str), stdin);
	printf("배열의 길이: %d\n", sizeof(str));					// 배열의 길이: 50
	printf("문자열 길이: %d / 문자열: %s", strlen(str), str); // 문자열 길이: 14 / 문자열: hi c language

	RemoveBSN(str);
	printf("문자열 길이: %d / 문자열: %s", strlen(str), str); // 문자열 길이: 13 / 문자열: hi c language
}
```

strlen의 반환형은 unsigned int지만 일반적으로 문자열의 길이는 int 타입에 저장 가능하므로 출력(%d)과 저장(int len)을 int형으로 하는 것이 흔하다. <br>

<h3> <strong> (3) 문자열 복사 함수 (strcpy, strncpy) </strong> </h3>

아래 함수들은 문자열을 복사하는 함수들이다. 

* <b>char* strcpy(char* dest, const char* src);</b>
* <b>char* strncpy(char* dest, const char* src, size_t n);</b>

strcpy는 복사받을 문자열과 복사할 문자열을 입력으로 받고, strncpy는 복사받을 문자열, 복사할 문자열, 그리고 복사할 최대 길이를 입력으로 받는다. <br>
단, strncpy의 경우 null문자를 고려하지 않고 길이를 고려하기 때문에 strlen(str)-1만큼 복사를 받고 str[sizeof(str)-1]=0을 사용해 null문자를 추가해줘야 한다.

```(c)
#include <stdio.h>
#include <string.h>

int main(void)
{
	char str1[20] = "1234567890";
	char str2[20];
	char str3[5];

	strcpy(str2, str1);
	printf("str1->str2로 복사: %s\n", str2);                    // 1234567890 출력

	strncpy(str3, str1, sizeof(str3));
	printf("str1->str3로 복사, sizeof(str3) 사용: %s\n", str3); // 잘못된 복사로 인해 이상한 출력이 발생함
	
	strncpy(str3, str1, sizeof(str3)-1);
	str3[sizeof(str3) - 1] = 0;
	printf("str1->str3로 복사, sizeof(str3) 사용: %s\n", str3); // 1234로 올바른 출력
}
```

<h3> <strong> (4) 문자열을 이어주는 함수 (strcat, strncat) </strong> </h3>

아래 함수들을 사용하면 두 개의 문자열을 이어 붙일 수 있다.

* <b>char* strcat(char* dest, const char* src);</b>
* <b>char* strncat(char* dest, const char* src, size_t n);</b>

만약 str1뒤에 str2 문자열을 붙이고 싶다면 strcat(str1, str2) 형식으로 사용하면 된다. <br>
단, str1의 null 문자 위치부터 이어 붙인다.

* str1 = "01234\0", str2 = "56789\0" -> "0123456789\0"

strncat의 경우 strcat에 추가로 str2에서 가져올 문자열의 최대 길이를 입력해야 한다. <br>
단, null 문자를 포함하지 않은 길이임을 참고하자.

<h3> <strong> (5) 문자열 비교 함수 (strcmp, strncmp) </strong> </h3>

만약 두 개의 문자열 변수가 다음과 같이 선언되어 있다 가정하자.

```(c)
char str1[] = "Hi C";
char str2[] = "Hi C";
```

이때 str1 == str2라는 연산을 수행하는 것은 str1과 str2가 가리키는 주소값이 같은지를 판단한다. <br>
즉, 해당 코드로는 문자열의 값이 같은지 비교할 수 없다. <br>
이를 가능하게 하는 것이 아래 함수들이다.

* <b>int strcmp(const char* s1, const char* s2)</b>
* <b>int strncmp(const char* s1, const char* s2)</b>

위 두 함수는 문자열이 같으면 0을 반환하고 그렇지 않으면 0이 아닌 수를 반환한다. <br>
strncmp의 경우 세 번째 인자로 전달된 수의 크기만큼 문자를 비교하여 <b>앞부터 중간부분까지 부분적으로 문자열 비교가 가능</b>하다. <br>

```(c)
#include <stdio.h>
#include <string.h>

int main(void)
{
	char str1[20] = "1234567890";
	char str2[20] = "1234567890";
	char str3[20] = "12356";

	printf("str1, str2 비교: %d\n", strcmp(str1, str2));					//0
	printf("str1, str3 비교: %d\n", strcmp(str1, str3));				    //-1
	printf("str2, str3 앞 3개의 문자만 비교: %d\n", strncmp(str2, str3, 3)); // 0
```

<h3> <strong> (6) 문자열 형 변환 함수 </strong> </h3>

<b><stdlib.h>헤더</b>파일에는 다음과 같은 함수들이 정의되어 있다.

* int atoi(const char* str);    // 문자열 내용을 ing형으로 변환한다.
* long atol(const char* str);   // 문자열 내용을 long형으로 변환한다.
* double atof(const char* str); // 문자열 내용을 

위에서 atoi는 ASCII to integer라는 뜻이고 아래 함수들 역시 integer를 long, double(float)로 바꾸면 동일하다. <br>
해당 함수들은 "123"을 정수로 바꾸거나 "12.34"를 실수형으로 변환할 때 사용할 수 있다.

```(c)
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
	char str[10];

	printf("문자열 정수 입력: ");
	fgets(str, sizeof(str), stdin);
	printf("변환된 정수: %d\n", atoi(str));				
}
```