<h2> <strong> 2. 문자열 </strong> </h2>

<h3> <strong> (1) 문자열 선언 </strong> </h3>

위와 같은 1차원 배열의 자료형을 char로 설정하면 문자열의 저장 및 변경이 가능해진다. <br>
단, 문자열을 저장할 때는 자동으로 <b>"\0"(escape sequence)</b>가 자동으로 삽입되기 때문에 <b>"문자열 길이 + 1"</b>로 길이를 설정해야 한다. <br>
이때 삽입되는 문자열을 <b>"null 문자"</b>라고 한다.

다음은 문자열 저장 및 수정, 그리고 null 문자를 확인하는 코드다.

```(c)
#include <stdio.h>

int main(void)
{
	char str[]="Hello C";
	printf("문자열의 길이: %d\n", sizeof(str) / sizeof(char)); // 8
	str[5] = '!'; str[6] = '!';
	printf("%s", str);
	printf('\n');
}
```

이때 <b>null문자의 아스키 코드는 0이며 공백 문자인 32와 다르니 주의해야 한다.</b> 

<h3> <strong> (2) 문자열 입력 </strong> </h3>

문자열은 scanf 함수의 서식 문자 %s를 이용해 입력받을 수 있다.

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main(void)
{
	char str[100];
	int idx = 0;

	printf("문자열을 입력해주세요: ");
	scanf("%s", str);
	
	printf("문자열 출력: %s", str);
}
```

이때 위에서 입력받은 문자열 역시 null 문자가 끝에 삽입된다. <br>
즉, null 문자는 문자열이여야 존재하고 문자열이 아니면 존재하지 않는 문자다. <br>
따라서 아래와 같은 배열을 문자열이 될 수 없다.

* char arr[] = {'H', 'i'};

단, 아래의 배열은 문자열이 될 수 있다.

* char arr[] = {'H', 'i', '\0'};