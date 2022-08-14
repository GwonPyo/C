<h2> <strong> 3. 조건부 컴파일 </strong> </h2>

<h3> <strong> (1) #if...#endif: 참이라면 </strong> </h3>

#if...#endif는 조건부 코드 삽입을 위한 지시자다. <br>
아래는 해당 지시자를 사용한 예시 코드다

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

#define ADD 1
#define MIN 0

int main(void)
{
	int num1, num2;
	printf("두 정수 입력: ");
	scanf("%d %d", &num1, &num2);

#if ADD
	printf("%d+%d=%d\n", num1, num2, num1 + num2);
#endif

#if MIN
	printf("%d-%d=%d\n", num1, num2, num1 + num2);
#endif

	return 0;
}
```

#if...#endif는 위와 같이 정의되어 있는 매크로가 참일 시 사이에 있는 코드를 삽입하고 거짓이면 삭제한다. <br>

<h3> <strong> (2) #ifdef...#endif: 정의되었다면 </strong> </h3>

#if는 참인지 거짓인지를 기준으로 동작했지만 #ifdef의 경우 정의되었는지 아닌지를 기준으로 동작한다. <br>
이때 매크로의 값은 중요하지 않기 때문에 아래와 같이 매크로의 몸체(값)은 생략해도 문제가 없다.

* #define ADD

단, 위와 같은 방식으로 정으되면 소스코드에 있는 매크로는 공백으로 대체된다. <br>

<h3> <strong> (3) #ifndef...#endif: 정의되지 않았다면 </strong> </h3>

#ifdef와 다르게 정의되어있지 않다면 사이에 있는 코드들을 삽입하고 정의되었다면 삭제한다.

<h3> <strong> (4) #else </strong> </h3>
if...else와 동일하게 #if, #ifdef, #ifndef문에도 #else를 추가할 수 있다.<br>
아래는 해당 지시자의 예시 코드다.

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

// #define ADD 1
#define MIN 1

int main(void)
{
	int num1, num2;
	printf("두 정수 입력: ");
	scanf("%d %d", &num1, &num2);

#ifdef ADD
	printf("%d+%d=%d\n", num1, num2, num1 + num2);
#else
	printf("정의되지 않았습니다.\n");
#endif

#if MIN == 0
	printf("%d-%d=%d\n", num1, num2, num1 - num2);
#else
	printf("정의되지 않았습니다.\n");
#endif

	return 0;
}
```