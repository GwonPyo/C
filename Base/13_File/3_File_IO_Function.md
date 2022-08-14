<h2> <strong> 3. 파일 입출력 관련 함수 </strong> </h2>

<h3> <strong> (1) 파일 입출력 기본 함수 </strong> </h3>

아래는 이전에 배웠던 문자열, 문자 출력 함수다. <br>
해당 함수들은 파일 입출력에 사용 가능하다.

* int fputc(int c, FILE* stream);
* int fgetc(FILE* stream);
* int fputs(const char* s, FILE* stream);
* char* fgets(char* s, int n, FILE* stream);

아래는 위 함수들의 예시 코드다.

```(c)
#include <stdio.h>

int main(void)
{	
	FILE* fw = fopen("text.txt", "wt");
	if (fw == NULL) {
		puts("파일 오픈 실패");
		return -1;
	}

	fputc('A', fw);
	fputc('B', fw);
	fputs("Hello File Stream1\n", fw);
	fputs("Hello File Stream2\n", fw);

	fclose(fw);

	FILE* fr = fopen("text.txt", "rt");
	if (fr == NULL) {
		puts("파일 오픈 실패");
		return -1;
	}

	for (int i = 0; i < 2; i++) 
		printf("%c\n", fgetc(fr));

	char str[100];
	for (int i = 0; i < 2; i++) {
		fgets(str, 100, fr);
		printf("%s", str);
	}
	fclose(fr);

	return 0;
}
```

위 예제의 출력결과를 보면 <b>파일은 문자열을 개행을 기준으로 구분한다</b>는 사실을 알 수 있다. <br>

<h3> <strong> (2) feof 함수 </strong> </h3>

파일의 전체 데이터를 가져와야 하는 경우 <b>feof 함수</b>를 사용할 수 있다.

* int feof(FILE* stream);

feof 함수는 인자로 전달된 FILE 포인터를 대상으로, <b>더 이상 읽을 데이터가 존재하지 않으면 0이 아닌 값을 반환한다.</b> <br>
즉, <b>파일의 끝을 확인해 하는 경우 유용하게 사용된다.</b>
아래는 feof 함수 사용 예시코드다.

```(c)
#include <stdio.h>

int main(void)
{	
	FILE* src = fopen("text.txt", "rt");
	FILE* des = fopen("feof.txt", "wt");

	if (src == NULL || des == NULL) {
		puts("파일 오픈 실패");
		return -1;
	}

	int ch;
	while ((ch = fgetc(src)) != EOF)
		fputc(ch, des);

	if (feof != 0)
		puts("파일 복사 완료");
	else
		puts("파일 복사 실패");

	fclose(src);
	fclose(des);

	return 0;
}
```

위 방법 외에도 fgets를 사용하여 문자열 단위로 데이터를 가져오는 방법도 있다. <br>

<h3> <strong> (3) 바이너리 데이터 입출력 </strong> </h3>

바이너리 데이터의 입력을 위해서는 <b>fread 함수</b>를 사용한다.

* <b>size_t fread(void* buffer, size_t size, size_t count, FILE* stream)</b>

fread 함수는 아래 방식으로 호출된다.

```(c)
int buf[10];
fread((void*) buf, sizeof(int), 10, f);
```

위 호출문의 의미는 다음과 같다.

* f로부터 sizeof(int)크기의 데이터 10개를 읽어들이고 buf에 저장해라.

이후 fread함수는 읽어 들인 데이터의 갯수 10를 반환하게 된다.<br>
만약 데이터를 읽는데 실패한다면 10보다 작은 값을 반환한다.

아래는 바이너리 데이터의 출력에 사용하는 <b>fwrite 함수</b>의 형태다.

* <b>size_t fwrite(const void* buffer, size_t size, size_t count, FILE* stream)</b>

해당 함수는 아래와 같이 호출하면 된다.

```(c)
int buf[5] = {1, 2, 3, 4, 5};
fread((void*) buf, sizeof(int), 5, f);
```

위 호출문의 의미는 다음과 같다.

* buf에 저장된 sizeof(int) 크기 데이터 5개를 f에 저장해라.

<h3> <strong> (4) 텍스트/바이너리 데이터 동시 입출력 </strong> </h3>

fprintf 함수는 텍스트와 바이너리 데이터를 동시에 출력해준다.

* <b>fprintf(f, "%s %d", name, age);</b>

아래는 fprintf 함수 사용 예시 코드다.

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>

void RemoveNewLine(char* str) {
	int len = strlen(str);
	str[len - 1] = 0;
}

void ClearInputBuffer() {
	while (getchar() != '\n');
}

int main(void)
{	
	FILE* f = fopen("fprintf.txt", "wt");

	if (f == NULL) {
		printf("파일 오픈 실패");
		return -1;
	}

	char name[5];
	int age;

	for (int i = 0; i < 3; i++) {
		printf("이름: "); fgets(name, 10, stdin);
		RemoveNewLine(name);
		
		printf("나이: "); scanf("%d", &age);
		fprintf(f, "%s %d\n", name, age);
		ClearInputBuffer();
	}
	fclose(f);
	return 0;
}
```

텍스트와 바이너리 데이터를 파일에서 동시에 받아오기 위해서는 fscanf 함수를 사용한다.

* <b>fscanf(f, "%s %d", name, age);</b>

다음은 fscanf 함수 활용 예시다.

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main(void)
{	
	FILE* f = fopen("fprintf.txt", "rt");

	if (f == NULL) {
		printf("파일 오픈 실패");
		return -1;
	}

	char name[10];
	int age;

	while (1) {
		int ret = fscanf(f, "%s %d", name, &age);
		if (ret == EOF)
			break;
		printf("이름: %s / 나이: %d\n", name, age);
	}
	fclose(f);
}
```

<h3> <strong> (5) 구조체 데이터 입출력 </strong> </h3>

구조체 데이터의 경우 구조체의 멤버 각각을 텍스트 및 바이너리 데이터로 저장하는 것보다 <b>구조체 자체를 바이너리 데이터로 처리</b>하면 된다. <br>
예시는 아래와 같다.

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

typedef struct {
	char name[10];
	int age;
} Person;

int main(void)
{	
	FILE* fw = fopen("struct.bin", "wb");

	if (fw == NULL) {
		printf("파일 오픈 실패");
		return -1;
	}

	Person person1;

	printf("이름, 나이를 입력해주세요: ");
	scanf("%s %d", person1.name, &person1.age);
	fwrite((void*)&person1, sizeof(Person), 1, fw);
	fclose(fw);

	FILE* fr = fopen("struct.bin", "rb");

	if (fr == NULL) {
		printf("파일 오픈 실패");
		return -1;
	}

	Person person2;
	fread((void*)&person2, sizeof(Person), 1, fr);
	printf("이름: %s / 나이: %d", person2.name, person2.age);
	fclose(fr);
}
```

<h3> <strong> (6) 파일 위치 지시자 </strong> </h3>

FILE 구조체 멤버에는 <b>파일의 위치 정보를 저장하는 멤버</b>가 존재하며 fgets, fputs 같은 함수가 호출될 때마다 갱신된다. <br>
우리는 이 멤버에 저장된 위치 정보를 통해 데이터를 읽고 쓸 위치를 변경할 수 있다.

파일 위치 지시자를 직접 이동시키려고 하려면 fseek 함수를 사용해야 한다. <br>
fseek 함수의 구성은 다음과 같다.

* <b>int fseek(FILE* stream, long offset, int wherefrom);</b>

fseek 함수는 성공 시 0, 실패 시 0이 아닌 값을 반환하며 위 수식의 의미는 다음과 같다.

* stream으로 전달된 파일 위치 지시자를 wherefrom에서부터 offset 바이트만큼 이동시켜라.

wherefrom 매개변수로 가능한 값으로는 아래 값들이 있다.

|매개변수|가리키는 위치|
|:---:|:---:|
|SEEK_SET(0)|파일 맨 앞부터 이동 시작|
|SEEK_CUR(1)|현재 위치부터 이동 시작|
|SEEK_END(2)|파일 맨 끝부터 이동 시작|

단, SEEK_END의 경우 EOF부터 이동을 시작하니 주의하자.<br>
offset의 경우 음수도 가능하고 양수도 가능하다. <br>

```(c)
#include <stdio.h>

int main(void)
{	
	FILE* fw = fopen("fseek.txt", "wt");
	fputs("0123456789", fw);
	fclose(fw);

	FILE* fr = fopen("fseek.txt", "rt");
	
	/*SEEK_END*/
	fseek(fr, -1, SEEK_END);
	putchar(fgetc(fr)); // 9
	
	/*SEEK_SET*/
	fseek(fr, 2, SEEK_SET);
	putchar(fgetc(fr)); // 2

	/*SEEK_CUR*/
	fseek(fr, 3, SEEK_CUR);
	putchar(fgetc(fr)); // 6

	fclose(fr);
	return 0;
}
```

만약 파일 위치 지시자의 값을 확인하고 싶다면 ftell 함수를 사용하면 된다.

* long ftell(FILE* stream);

ftell 함수는 처음 위치를 0으로 반환하고 이후 위치들은 1씩 증가하는 값으로 위치를 반환한다. <br>
즉, 첫 번째 바이트는 0, 두 번째 바이트는 1, 세 번째 바이트는 2를 반환하는 형식으로 진행된다. <br>
아래는 ftell 함수 예시 코드다.

```(c)
#include <stdio.h>

int main(void)
{	
	FILE* fw = fopen("ftell.txt", "wt");
	fputs("1234-", fw);
	fclose(fw);

	FILE* fr = fopen("ftell.txt", "rt");

	for (int i = 0; i < 4; i++) {
		putchar(fgetc(fr));
		long fpos = ftell(fr);
		fseek(fr, -1, SEEK_END);
		putchar(fgetc(fr));
		fseek(fr, fpos, SEEK_SET);
	}
	fclose(fr);
	return 0;
}
```