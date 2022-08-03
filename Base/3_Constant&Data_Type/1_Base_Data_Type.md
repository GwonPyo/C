<h2> <strong> 1. 기본 자료형 </strong> </h2>

<h3> <strong> (1) 기본 자료형의 종류 </strong> </h3>

C언어가 제공하는 기본 자료형은 다음과 같다.

|종류|자료형|크기|
|:---:|:---:|:---:|
|정수형|char <br> short <br> int <br> long <br> long long|1바이트 <br> 2바이트 <br> 4바이트 <br> 4바이트 <br> 8바이트|
|실수형|float <br> double <br> long double|4바이트 <br> 8바이트 <br> 8바이트 이상|

자료형이 존재하는 이유는 다음과 같다.

* <b>데이터의 표현 형식</b> <br>
데이터는 크게 정수형과 실수형 데이터로 나뉜다. <br>
즉, 정수와 실수를 표현하는 방식이 다르므로 정수와 실수를 표현하는 자료형은 서로 달라야한다.

* <b>메모리 공간의 활용</b> <br>
작은 정수 여러 개를 저장해야 한다면 longlong이나 int로 저장하는 것보다는 char이나 short로 저장하는 것이 훨씬 효율적이다. <br>
따라서 같은 데이터 타입이라도 메모리 효율을 위해 여러 자료형이 필요하다.

<h3> <strong> (2) sizeof </strong> </h3>

<b>sizeof()</b> 연산자를 사용하면 변수, 상수, 자료형 등의 메모리 크기를 알 수 있다. <br>
사용법은 다음과 같다.

* sizeof(변수, 상수, 자료형 중 택1)

다음은 사용 예시 코드다.

```(c)
#include <stdio.h>

int main(void)
{
	printf("char 크기: %d\n", sizeof(char)); 
	printf("short 크기: %d\n", sizeof(short));
	printf("int 크기: %d\n", sizeof(int));
	printf("long 크기: %d\n", sizeof(long));
	printf("long long 크기: %d\n", sizeof(long long));
	
	float f = 0.1;
	double d = 0.1;
	long double ld = 0.1;
	printf("float 크기: %d\n", sizeof(f));
	printf("double 크기: %d\n", sizeof(d));
	printf("long double 크기: %d\n", sizeof(ld));
}
```

<h3> <strong> (3) 연산 방식 </strong> </h3>

char형 num1, num2와 short형 num3, num4가 있다고 하자. <br>
각각의 쌍을 더하면 각각 char, short 자료형으로 출력될 것이라 생각하기 쉽지만 int형 상수가 반환된다. <br>
컴퓨터의 CPU가 처리하기에 가장 적합한 크기의 정수 자료형은 int이다. <br>
따라서 int형 연산의 속도가 다른 자료형의 연산 속도보다 빨라 <b>int보다 작은 자료형은 int로 변환되어 연산</b>된다.

실수형의 경우 float연산 결과는 float, double은 double로 반환된다. <br>
하지만 실수형의 경우 보편적으로 double형을 사용하는데 이유는 다음과 같다.

|자료형|정밀도|바이트|
|:---:|:---:|:---:|
|float|6자리|4바이트|
|double|15자리|8바이트|
|long double|18자리|12바이트|

위 표에서 정밀도는 <b>오차가 발생하지 않는 소수점 이하의 자릿수</b>를 의미한다. <br>
즉, double은 float에 비해 정밀도가 높다. <br>
long double은 정밀도가 높긴하지만 시스템에 따라 12바이트인 경우가 있는데 12바이트는 너무 부담스러운 크기이므로 주로 double형을 사용하는 것이다.

다음은 예시 코드이다.
```(c)
#include <stdio.h>

int main(void)
{
	char num1 = 1, num2 = 2;
	printf("char 연산 결과: %d\n", sizeof(num1 + num2));// 4
	float f1 = 0.1, f2 = 0.4;
	printf("float 연산 결과: %d\n", sizeof(f1 + f2));   // 4
	double d1 = 0.1, d2 = 0.4;
	printf("double 연산 결과: %d\n", sizeof(d1 + d2));  // 8
}
```

<h3> <strong> (4) unsigned </strong> </h3>

<b>정수 자료형</b>의 앞에 unsigned를 추가하면 0이상의 값만 표현할 수 있다. <br>
unsigned를 사용하면 양의 정수만 표현하기 때문에 부호가 필요없으므로 MSB 비트를 제거하고 크기를 나타내는 비트로 사용한다. <br>
즉, <b>양의 정수의 범위를 두 배 넓게 표현</b>할 수 있다. <br>
따라서, char의 경우 기존에 -128\~127만 표현 가능하지만 unsigned char의 경우 0\~255까지 표현 가능하다.

|종류|자료형|크기|
|:---:|:---:|:---:|
|정수형|char <br> unsigned short <br> unsigned int <br> unsigned long <br> unsigned long long|1바이트 <br> 2바이트 <br> 4바이트 <br> 4바이트 <br> 8바이트|
