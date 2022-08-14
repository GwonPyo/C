<h2> <strong> 1. 파일 입출력 </strong> </h2>

<h3> <strong> (1) 파일 스트림 </strong> </h3>

이전에 스트림에 대해 배웠던 것처럼 임의의 파일을 읽어야 할 때는 <b>프로그램과 파일 사이에 스트림을 형성해야 한다.</b> <br>
스트림 생성을 위해는 다음 함수를 사용한다.

* <b>FILE* fopen(const char* filename, const char* mode);</b>

fopen 함수는 첫 번째 인자로 파일명, 두 번째 인자로 형성할 스트림 종류를 넘겨주면 FILE 구조체 변수가 반환된다. <br>
이때 생성된 구조체 변수는 파일에 대한 정보를 담고있다.

<h3> <strong> (2) 입력 스트림&출력 스트림 </strong> </h3>

이제 파일 스트림을 직접 생성해보자. <br>
스트림은 크게 입력과 출력 스트림으로 나뉘며 파일 입력 스트림은 파일의 데이터를 읽기 위한, 출력 스트림은 파일에 데이터를 쓰기 위한 스트림이다. <br>
아래는 입력/출력 스트림을 생성하는 코드다.

* FILE* f = fopen("text.txt", <b>"wt"</b>); // 출력 스트림 형성
* FILE* f = fopen("text.txt", <b>"rt"</b>); // 입력 스트림 형성

아래는 출력 스트림 형성 예시 코드다.

```(c)
#include <stdio.h>

int main(void)
{	
	FILE* f = fopen("text.txt", "wt");
	if (f == NULL) {
		puts("파일 오픈 실패");
		return -1;	// 비정상적 종료
	}

	fputs("File Open1\n", f);
	fputs("File Open2\n", f);
	fputs("File Open3\n", f);
	fclose(f);
	return 0;
}
```

위의 fclose함수의 구성은 다음과 같다.

* int fclose(FILE* stream);

사용이 끝난 스트림은 fclose 함수로 꼭 종료해 주는 것이 좋다.

> <b>참고</b> <br>
fclose 함수를 사용해야 하는 이유는 다음과 같다.
>
>* 자원의 낭비
>* 버퍼링된 데이터의 출력
>
> 운영체제는 스트림을 형성할 때 시스템의 자원을 사용하는데 이후에 사용할 일이 없는 스트림을 남겨두면 해당 자원은 의미없게 쓰이게 된다. <br>
또한 이전에 사용한 fputs와 같은 함수를 사용할 때 파일에 바로 작성하는 것이 아니라 중간 버퍼 저장 후 한번에 저장하는 과정을 거친다. <br>
즉, 갑작스럽게 프로그램이 종료되거나 컴퓨터가 꺼지는 등의 불상사가 생기면 버퍼링된 데이터는 사라진다. <br>
따라서 스트림의 사용이 끝났다면 fclose 함수를 사용해주자. <br>
만약 파일 스트림의 출력 버퍼를 비우고 싶다면 아래 함수를 사용하면 된다.
>
> * int fflush(FILE* stream);

아래는 입력 스트림을 형성하는 코드다.

```(c)
#include <stdio.h>

int main(void)
{	
	FILE* f = fopen("text.txt", "rt");
	if (f == NULL) {
		puts("파일 오픈 실패");
		return -1;	// 비정상적 종료
	}

	char str[100];
	for (int i = 0; i < 3; i++) {
		fgets(str, 100, f);
		fputs(str, stdout);
	}

	fclose(f);
	return 0;
}
```