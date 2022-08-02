<h2> <strong> 3. 키워드  </strong> </h2>

<h3> <strong> (1) scanf </strong> </h3>

scanf 함수를 사용하면 키보드로 여러 형태의 데이터를 입력 받을 수 있다. <br>
사용법은 다음과 같다.

* scanf("(입력받을 타입의 서식 문자)", &(변수 이름))

코드로 작성해보면 다음과 같이 작성할 수 있다.

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main(void)
{
	int num1, num2;

	scanf("%d %d", &num1, &num2);
	printf("num1+num2=%d", num1+num2);
}
```

만약 위 코드에서 <b>#define _CRT_SECURE_NO_WARNINGS</b>없이 visual studio를 이용해 디버깅을 하면 다음과 같은 에러가 발생한다. 

![scanf 에러](https://user-images.githubusercontent.com/85156021/182304999-f8f40563-b241-444e-ba97-10fb9aa90db6.PNG)

#include <studio.h> 밑에 써도 에러가 발생하니 맨 위에 쓰도록 하자.

<h3> <strong> (2) 키워드 </strong> </h3>

키워드란 int, scanf처럼 이미 기능적 의미가 정해져 C언어의 문법을 구성하는 단어들을 말한다. <br>
키워드들은 프로그래머가 다른 용도로 사용할 수 없도록 제한되어 있으며 함수나 변수의 이름으로도 사용할 수 없다.
