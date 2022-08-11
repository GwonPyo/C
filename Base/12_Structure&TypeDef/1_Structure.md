<h2> <strong> 1. 구조체 </strong> </h2>

<h3> <strong> (1) 구조체 개념 </strong> </h3>

<b>구조체(structure)</b>는 하나 이상의 변수(배열, 포인터 포함)를 묶어서 새로운 자료형을 정의하는 도구다. <br>
즉, 우리는 구조체를 사용해 새로운 자료형을 정의할 수 있다. <br>

예를 들어, 우리가 마우스 좌표정보를 저장하고 관리해야 한다면 아래와 같이 두 개의 변수를 선언할 것이다.

```(c)
int xpos;
int ypos;
```

하지만 위 두 개의 변수는 완전히 독립적인 변수가 아니라 마우스의 위치 정보를 함께 표현한다. <br>
즉, 마우스의 위치 정보를 갱신하거나 위치정보를 출력하는 등의 작업을 하려면 <b>두 개의 변수를 동시에 참조</b>해야 한다. 
따라서 위 두 변수를 하나로 묶는 것이 관리가 쉬울 것이다. <br>
이를 가능하게 해주는 것이 구조체다. <br>
아래는 위 두 변수를 하나의 구조체로 만든 코드다.

'''(c)
struct mouse_point{
    int xpos;
    int ypos;
}
```

이때 mouse_point가 int와 같은 자료형의 이름이 된다. <br>
구조체 안에는 위처럼 기본 자료형 뿐만 아니라 배열, 포인터 변수도 입력할 수 있다.

'''(c)
struct person{
    char name[6]; 
    char id[7];    
    int age
}
```

이렇게 기본 자료형 변수를 묶어 새로운 자료형을 만든 것을 <b>사용자 정의 자료형(user defined data type)</b>이라고 부른다. <br>

<h3> <strong> (2) 구조체 변수 </strong> </h3>

구조체 변수는 다음과 같이 선언한다.

* struct (구조체 이름) (변수 이름);

예를 들어, 위에서 만든 mouse_point 구조체 타입의 변수는 다음과 같이 선언할 수 있다. <br>

* struct mouse_point point;

만들어진 구조체 변수 point의 xpos, ypos 등의 <b>멤버에 접근할 때는 다음과 같이 '.'을 사용하여 접근</b>하면 된다. <br>

* point.xpos = 10;

아래는 입력받는 두 점 사이의 거리를 계산하는 구조체 예시 코드다.

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <math.h>

struct point {
	int xpos;
	int ypos;
}; // 구조체 정의

int main(void)
{
	struct point p1; // 입력 받을 첫 번째 점
	struct point p2; // 입력 받을 두 번째 점

	printf("첫 번째 점 좌표 입력: ");
	scanf("%d%d", &p1.xpos, &p1.ypos);

	printf("두 번째 점 좌표 입력: ");
	scanf("%d%d", &p2.xpos, &p2.ypos);

	double distance = sqrt((double)((p1.xpos - p2.xpos) * (p1.xpos - p2.xpos) + (p1.ypos - p2.ypos) * (p1.ypos - p2.ypos)));
	printf("두 점 사이의 거리: %.3f", distance);
}
```

이번에는 구조체에 정의된 배열을 사용하는 예시 코드를 살펴보자. 

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>

struct person {
	char name[6];
	char id[7];
	int age;
}; 

int main(void)
{
	struct person p1;
	struct person p2;

	/* p1 멤버들 값 갱신 */
	strcpy(p1.name, "nam");		// 배열이므로 문자열 저장을 위해서 strcpy를 사용해야 한다. 
	strcpy(p1.id, "123123");
	p1.age = 21;

	/* p2 멤버들 값 갱신 */
	printf("이름 입력: "); scanf("%s", p2.name);
	printf("번호 입력: "); scanf("%s", p2.id);
	printf("나이 입력: "); scanf("%d", &p2.age);

	printf("이름: %s / %s\n", p1.name, p2.name);
	printf("번호: %s / %s\n", p1.id, p2.id);
	printf("나이: %d / %d\n", p1.age, p2.age);
}
```

만약 구조체 선언시 구조체 변수를 동시에 선언하고 싶다면 아래와 같이 선언하면 된다. <br>

```(c)
struct point {
	int xpos;
	int ypos;
} pos1, pos2;
```

또한 구조체 변수를 선언과 동시에 초기화도 가능한데 이는 다음과 같이 수행할 수 있다.

* struct person p = {"nam", "123123", 21};

위처럼 초기화 시에는 문자열을 배열에 저장하기 위해 strcpy를 사용하지 않아도 된다.

<h3> <strong> (3) 구조체 배열 </strong> </h3>

구조체 배열은 아래와 같이 선언 가능하다.

* struct point points[5];

아래는 구조체 배열에 대한 코드 예시이다.

```(c)
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

struct point {
	int xpos;
	int ypos;
};

int main(void)
{
	struct point points[2];
	
	for (int i = 0; i < 2; i++) {
		printf("%d번째 좌표 입력: ", i+1);
		scanf("%d%d", &points[i].xpos, &points[i].ypos);
	}

	printf("\n---입력 받은 좌표 출력---\n");
	for (int i = 0; i < 2; i++)
		printf("%d번째 좌표: %d, %d\n", i + 1, points[i].xpos, points[i].ypos);
}
```

구조체 배열은 이전에 구조체 변수를 초기화했던 것처럼 아래와 같이 초기화가 가능하다. 

```(c)
struct point points[2] = {
		{1, 2},
		{3, 4}
	};
```

<h3> <strong> (3) 구조체 포인터 </strong> </h3>

구조체 포인터는 아래와 같이 선언 가능하다.

* struct point\* ptr;

위 포인터의 주소가 가리키는 구조체의 멤버는 다음과 같이 두 가지 방식으로 접근 가능하다.

* (\*ptr).xpos=0; (\*ptr).ypos=1;
* ptr->xpos=0; ptr->ypos=1;

아래는 구조체의 포인터 사용 예시다.

```(c)
#include <stdio.h>

struct point {
	int xpos;
	int ypos;
};

void change_point(struct point* ptr) {
	ptr->xpos += 10;
	ptr->ypos += 10;
}

int main(void)
{
	struct point pos = { 1, 2 };

	printf("변경 전 좌표: %d, %d\n", pos.xpos, pos.ypos);
	change_point(&pos);
	printf("변경 후 좌표: %d, %d", pos.xpos, pos.ypos);
}
```

추가적으로 <b>구조체 변수의 주소 값은 첫 번째 멤버의 주소값과 동일하다</b>는 사실을 기억해두자.