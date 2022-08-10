<h2> <strong> 2. 문자 관련 함수 </strong> </h2>

<h3> <strong> (1) 문자 입출력 함수 </strong> </h3>

다음은 문자 단위 출력 함수이다.

* int putchar(int c);
* int fputc(int c, FILE * stream);

<b>putchar 함수는 인자로 전달된 문자를 표준 출력 스트림으로 전달한다.</b> <br>
즉, 모니터에 인자로 전달된 문자를 출력한다.

fputc 함수도 putchar과 동일하지만 <b>문자를 전달할 스트림을 정할 수 있다.</b> <br>
즉, stdout뿐만 아니라 파일 스트림도 가능하다. <br>
스트림을 지정하기 위해 2번째 매개변수에 스트림을 전달하며 stdout을 전달하면 putchar과 동일한 역할을 한다.

위 두 함수는 모두 오류가 발생해 정상적인 결과를 보장하지 못한다면 <b>EOF를 반환한다.</b>

다음은 문자 단위 입력 함수이다.

* int getchar(int c);
* fgetc(FILE * stream);

<b>getchar는 표준 입력 스트림으로부터 하나의 문자를 입력 받아 반환한다. </b> <br>
fgetc 역시 문자를 입력 받는 함수지만 <b>문자를 입력받을 스트림을 지정할 수 있다.</b>

아래는 위 함수들을 사용한 예시 코드다.

```(c)
#include <stdio.h>

int main(void)
{
	int c1, c2;
	c1 = getchar();
	c2 = fgetc(stdin); // 이전 문자를 입력할 때 사용한 \n이 입력됨.

	putchar(c1);       
	fputc(c2, stdout); 
}
```

<h3> <strong> (2) EOF </strong> </h3>

EOF는 <b>End of File</b>의 약자로 파일의 끝을 표현하기 위해 정의한 상수다. <br>
예를 들어, fgetc() 함수를 이용해 파일을 읽을 때 EOF가 반환되면 파일의 끝에 도달해 더 이상 읽을 내용이 없다는 의미가 된다. <br>
단, 키보드 사용시 다음과 같은 경우에 EOF를 반환한다.

* 함수 호출 실패
* (window) ctrl+z / (linux) ctrl+d 입력

다음 코드로 EOF의 입력을 확인해 볼 수 있다.

```(c)
#include <stdio.h>

int main(void)
{
	int c;
	
	while (1) {
		c = getchar();
		if (c == EOF)
			break;
		putchar(c);
	}
}
```

위에서 콘솔에 hi, I love you와 같은 문자열을 입력해도 올바르게 출력되는 것을 확인할 수 있는다. <br> 
이는 문장이 입력되면 문장을 구성하는 문자의 수만큼 getchar 함수가 호출되기 때문에 문제가 없다.

><b>(참고)</b> <br>
getchar, putchar, fgetc, fputc 함수들은 모두 반환형이 int이고 입력 문자도 int형으로 받는다. <br>
이는 EOF가 -1 상수값을 가지기 때문이다. <br>
컴파일러마다 char을 unsigned char로 처리하는 경우가 있다. <br>
이런 경우 EOF가 이상한 값으로 변할 수 있기 때문에 어떠한 경우에도 -1을 인식할 수 있도록 int형으로 반환하는 것이다.