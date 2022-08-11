<h2> <strong> 2. Typedef </strong> </h2>

<h3> <strong> (1) Typedef 개념 및 선언 </strong> </h3>

이전에 구조체 변수를 선언할 때 아래처럼 구조체 이름 앞에 struct를 붙여야 했다.

* <b>struct</b> point pos;

이때 <b>typedef</b>선언을 추가하면 위의 struct의 선언을 없앨수 있다.

typedef는 아래와 같이 <b>기존에 존재하는 자료형의 이름에 새 이름을 부여하는 것을 목적</b>으로 한다.

* typedef int INT;

위 코드를 사용하면 INT가 기존 int의 또 다른 이름이 된다. <br>
즉, 아래와 같은 코드를 사용할 수 있다.

* INT num; // int num;과 동일한 표현

추가적으로 <b>typedef로 정의되는 자료형은 대문자로 시작하는 것이 관례</b>다.

<h3> <strong> (2) 구조체와 Typedef 선언 </strong> </h3>

다시 구조체 변수의 선언으로 돌아가보자. <br>
간단한 선언을 위해 struct를 지우려면 다음과 같은 방법을 사용하면 된다.

* typedef struct point Point;

즉, 아래와 같이 구조체 선언 이후에 typedef 선언을 해주면 된다.

```(c)
struct point{
    int xpos;
    int ypos;
}
typedef struct point Point;
```

위 코드는 아래와 같은 방식으로 표현할 수도 있다. (아래 방식이 더 보편적이다.)

```(c)
typedef struct point{
    int xpos;
    int ypos;
} Point;
```

또한 아래와 같이 <b>구조체의 이름을 생략</b>해서도 선언 가능하다.

```(c)
typedef struct{
    int xpos;
    int ypos;
} Point;
```

<h3> <strong> (3) 구조체의 크기 </strong> </h3>

아래는 구조체의 크기를 확인하는 코드이다.

```(c)
#include <stdio.h>

typedef struct {
	char name[6];
	char id[7];
	int age;
}Person;

int main(void)
{
	printf("구조체의 크기: %u\n", sizeof(Person)); // 20
}
```

직관적으로 Person 구조체는 6+7+4=17로 총 17의 크기를 가져야 하지만 결과로는 20이 출력된다. <br>
이는 구조체가 가장 큰 자료형의 크기에 맞춰 패딩되기 때문이다. <br>

* char 형은 6+7로 총 13 byte의 크기를 가진다. 이때 int형의 크기인 4byte에 맞추려면 총 16byte를 차지하도록 패딩되어야 한다.

즉, id 멤버의 크기를 7~10사이의 숫자로 바꾸면 결과는 그대로 20이고, 11로 바꾸면 결과는 24로 바뀐다. <br>

아래는 또 다른 예시이다.

```(c)
typedef struct {
	int num2;
	double num3;
}Nums1;

typedef struct {
	char num1;
	int num2;
	double num3;
}Nums2;

int main(void)
{
	printf("구조체의 크기: %u\n", sizeof(Nums1)); // 16
	printf("구조체의 크기: %u\n", sizeof(Nums2)); // 16
}
```