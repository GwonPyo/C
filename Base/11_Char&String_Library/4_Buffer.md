<h2> <strong> 4. 버퍼 </strong> </h2>

<h3> <strong> (1) 버퍼 </strong> </h3>

이전에 배운 printf, scanf, fputc, fputs 등을 <b>표준 입출력 함수</b>라고 부른다.<br>
이러한 함수를 통해 데이터를 입출력하면 <b>해당 데이터들은 운영체제가 제공하는 메모리 버퍼를 통과한다.</b> <br>
메모리 버퍼란 <b>'데이터를 임시로 모아두는 메모리 공간'</b>으로 입출력 스트림의 중간에 위치한다. <br>

예시를 들어보자. <br>
우리가 fgets 함수를 사용하면 문자열을 입력해야 한다. <br>
문자열을 입력하고 엔터키를 누르면 입력 스트림을 거쳐 입력버퍼로 문자열이 들어간다. <br>
즉, 엔터 키가 눌리기 전에는 입력버퍼가 비워져 있으므로 아무리 문자열을 입력해도 fgets 함수는 문자열을 읽지 못한다.

* 입력 버퍼에 문자열이 들어가는 때는 엔터 키를 누른 시점이다.

<h3> <strong> (2) 출력버퍼를 비우는 함수 </strong> </h3>

* int fflush(FILE* stream);

위 함수를 이용하면 출력버퍼를 비울 수 있다. <br>
즉, fflush(stdout);을 사용하면 표준 출력버퍼를 비운다.<br>
이때 **출력버퍼를 비운다는 것은 출력버퍼에 저장된 데이터를 목적지로 이동시킨다는 의미다.** 

<h3> <strong> (3) 입력버퍼를 비우는 함수 </strong> </h3>

출력버퍼를 비우는 것은 데이터를 목적지로 전송함을 의미하지만 **입력버퍼를 비우는 것은 데이터의 소멸을 의미한다.** <br>
아래 코드를 살펴보자.

```(c)
#include <stdio.h>

int main(void)
{
	char id[7];
	char name[5];

	fputs("6자리 ID 입력: ", stdout);
	fgets(id, sizeof(id), stdin);

	fputs("이름 입력: ", stdout);
	fgets(name, sizeof(name), stdin);

	printf("입력받은 ID: %s\n", id);
	printf("입력받은 이름: %s\n", name);
}
```

위 코드를 실행하면 결과는 다음과 같다.

(사진1)

위 코드의 문제는 ID를 입력할 때 남아있는 개행 문자를 이름을 입력 받을 때 받아준다는 것이다. <br>
fgets는 \n 문자를 만나면 종료되는 함수이므로 개행 문자만 name에 저장되게 된다. <br>
만약 입력으로 1234567890123이 들어가면 어떨까? <br>
123456이 id에 저장되고 7890이 name에 저장될 것이다. <br>
즉, 우리가 원하는 코드를 위해서는 이전에 id를 입력받을 때 <b>버퍼에 남아있는 나머지 문자열을 모두 제거하는 것</b>이다 <br>
이는 아래 코드와 같이 입력버퍼에 저장된 문자를 모두 읽어들여 해결할 수 있다. <br>

```(c)
#include <stdio.h>

void ClearInputBuffer(void) {
	while (getchar() != '\n');
}

int main(void)
{
	char id[7];
	char name[5];

	fputs("6자리 ID 입력: ", stdout);
	fgets(id, sizeof(id), stdin);
	ClearInputBuffer();

	fputs("이름 입력: ", stdout);
	fgets(name, sizeof(name), stdin);

	printf("입력받은 ID: %s\n", id);
	printf("입력받은 이름: %s\n", name);
}
```

해당 기법을 사용하면 아래와 같이 정상적인 결과를 출력한다.

(사진2)