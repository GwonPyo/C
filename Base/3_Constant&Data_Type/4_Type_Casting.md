<h2> <strong> 4. 자료형 변환 </strong> </h2>

char형 데이터를 int형으로 바꾸거나, float형 데이터를 int형으로 바꾸는 과정을 <b>자료형 변환</b>이라고 부른다. <br>
자료형 변환은 두 가지로 구분된다.

* <b> 자동 형 변환(묵시적 형 변환, explicit type casting) </b>
* <b> 강제 형 변환(명시적 형 변환, implicit type casting) </b>

<h3> <strong> (1) 자동 형 변환 </strong> </h3>

자동 형 변환이란 자동으로 발생하는 형 변환을 말한다. <br>
자동 형 변환은 다음과 같은 경우 발생한다.

> <b>[1] 대입연산</b> <br>
일반적으로 대입 연산자의 두 피연산자의 자료형이 동일하지 않은 경우 왼쪽의 피연산자를 기준으로 형 변환이 일어난다. <br>
> * double num = 123; 
> 
> 위의 경우 변수 num은 double형이지만 123은 int형 리터럴이다. <br>
이런 경우 <b>int형 리터럴이 double형으로 변환</b>되어 num에 저장된다. <br>
다음 경우를 살펴보자.
> * int num = 3.14;
>
> 위 경우 <b>double형 리터럴을 int형으로 변환</b>한 후에 변수 num에 저장하게 된다. <br>
위처럼 실수형이 정수형으로 변환되는 경우 소숫점 아래를 버리고 정수부분만 남게된다. <br>
즉, num에는 정수 3이 저장된다. <br>
마지막으로 아래와 같이 해당 자료형의 범위를 넘어가는 수를 저장하려고 하면 어떨지 확인해보자.
> * int num = 128; char ch = num; 
> 
> 128을 비트로 나타내면 다음과 같다.
> * 128 -> 00000000 00000000 00000000 10000000
>
> 이때 우리는 위 4바이트의 데이터를 1바이트로 줄여서 10000000를 변수 ch에 저장한다. <br>
하지만 10000000은 1바이트에서 -128을 의미하므로 ch에는 -128이 저장되게 된다. <br>
즉, 위처럼 <b>상위 바이트의 손실</b>이 발생할 경우 부호가 바뀌므로 주의해야 한다.
>
> <b>[2] 정수의 승격</b> <br>
정수형 데이터는 연산시 int형으로 자동 형변환 된다는 사실을 배웠었다. <br>
이러한 형태의 형 변환을 <b> 정수의 승격(Integral Promotion)</b>이라고 부른다.
즉 아래 경우에도 자동 형 변환이 발생한다.
>```(c)
>#include <stdio.h>
>
>int main(void)
>{
>	short num1 = 1, num2 = 2;
>	short num3 = num1 + num2; // int형으로 변화된 후 연산 진행, int형인 결과 데이터가 short로 형 변환 된 후 대입
>}
>```
>
> <b>[3] 피연산자 자료형 불일치</b> <br>
아래와 같은 경우를 살펴보자.
> * double num = 1.23 + 1;
>
> 위처럼 산술 연산자에 사용되는 두 개의 피연산자가 자료형이 일치하지 않으면 자동 형 변환이 발생한다. <br>
이때, 피연산자의 자료형이 일치하지 않아 발생하는 자동 형 변환은 <b> 데이터의 손실을 최소화하는 방향</b>으로 진행된다. <br>
데이터 손실 최소화 기준은 다음과 같다.
> * int -> long -> long long -> float -> double -> long double

<h3> <strong> (2) 강제 형 변환 </strong> </h3>

강제 형 변환(묵시적 형 변환)은 <b>형 변환 연산자를 사용해 강제로 형 변환을 하는 명령</b>을 의미한다. <br>
아래 코드를 살펴보자.

```(c)
#include <stdio.h>

int main(void)
{
	int num1 = 1, num2 = 2;
	double result = num1 / num2;
	printf("result: %f", result); // result: 0.000000
}
```

위 경우 우리는 일반적으로 0.5라는 값을 얻기를 원한다. <br>
하지만 해당 코드는 다음과 같은 과정을 거쳐 0이라는 값을 도출한다. <br>

1. num1 / num2 연산을 진행한다. 이때 num1과 num2가 int형이므로 연산의 결과는 0이 된다.
2. 해당 값을 double형으로 변환하여 변수에 저장한다.

만약 우리가 num1을 double형으로 바꾸고 연산을 진행할 수 있다면 이전에 배운 자동 형 변환의 원리로 올바른 값을 얻을 수 있다. <br>
아래 코드를 확인하자.

```(c)
#include <stdio.h>

int main(void)
{
	int num1 = 1, num2 = 2;
	double result = (double)num1 / num2;
	printf("result: %f", result); // result: 0.500000
}
```

위와 같은 (double) 연산자를 <b>형 변환 연산자(type casting operator)</b>라고 부른다.

추가적으로 아래와 같이 자동형 변환이 일어나는 경우 형 변환 연산자를 명시해 주는 것이 좋다고 한다.

* int num1 = 1; double num2 = 1.2 * num1 <br>
-> int num1 = 1; double num2 = 1.2 * (double)num1
