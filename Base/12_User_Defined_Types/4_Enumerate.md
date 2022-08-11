<h2> <strong> 4. 열거형 </strong> </h2>

구조체와 공용체는 저장할 값의 유형을 멤버의 자료형으로 결정했지만, 열거형은 <b>저장 가능한 값 자체를 정수 형태로 결정한다.</b>
열거형은 다음과 같이 선언 가능하다.

* enum color {RED, ORANGE, YELLOW, GREEN};

위 경우 RED부터 GREEN은 0부터 1씩 증가하는 값을 가지며 <b>해당 값들은 상수다.</b>  <br>
즉, 아래 선언과 동일하다.

* enum color {RED=0, ORANGE=1, YELLOW=2, GREEN=3};

아래와 같은 선언도 가능하다.

* enum color {RED=1, ORANGE, YELLOW=4, GREEN};

위 경우는 아래와 같이 이전 값에 +1을 한 형태로 저장된다.

* enum color {RED=1, ORANGE=2, YELLOW=4, GREEN=5};

아래 경우에도 동일하게 이전 값에 +1을 한 형태로 저장된다.

* enum color {RED=1, ORANGE, YELLOW=2, GREEN}  <br>
-> enum color {RED=1, ORANGE=2, YELLOW = 2, GREEN=3}

추가적으로 열거형에 사용한 상수들은 아래처럼 프로그램 상에서도 상수로 사용가능하다.

```(C)
#include <stdio.h>

typedef enum color {
	RED = 1, ORANGE, YELLOW = 4, GREEN
} Color;

int main(void)
{
	printf("%d\n", RED); // 1
}
```