<h2> <strong> 3. 공용체 </strong> </h2>

공용체는 구조체의 선언과 비슷하다. <br>
기존에 사용했던 struct선언을 union으로만 바꿔주면 된다. <br>
아래는 동일한 내용의 구조체와 공용체의 차이를 비교해보는 코드다.

```(c)
typedef struct {
	char name[6];
	char id[7];
	int age;
}S_Person;

typedef union {
	char name[6];
	char id[7];
	int age;
}U_Person;

int main(void)
{
	printf("구조체의 크기: %u\n", sizeof(S_Person)); // 20
	printf("구조체의 크기: %u\n", sizeof(U_Person)); // 8, 만약 id의 길이가 9라면 12가 된다.
}
```

공용체의 크기는 가장 큰 자료형(int)에 맞춰 패딩된 멤버중 가장 큰 멤버의 크기와 동일하다. <br>
이번에는 공용체와 공용체 멤버들의 주소 값을 뽑아보자.

```(c)
#include <stdio.h>

typedef union {
	char name[6];
	char id[7];
	int age;
}U_Person;

int main(void)
{
	U_Person person;
	printf("구조체 주소: %p\n", &person); 
	printf("name 주소: %p\n", &person.name); 
	printf("id 주소: %p\n", &person.id);
	printf("age 주소: %p\n", &person.age);
}
```

위 코드를 실행해보면 4개의 변수 모두 동일한 주소값을 가진다. <br>
즉, 위 내용을 모두 종합해보면 <b>공용체의 멤버들은 모두 같은 메모리 공간을 공유</b>한다. (가장 큰 멤버의 크기를 메모리 공간으로 가지고 있으니 문제가 없다.) <br>
<br>공용체는 위와 같은 특성 때문에 하나의 메모리 공간을 둘 이상의 접근 방식으로 접근할 때 유용하다.</br>

> Ex) int형 정수를 입력 받고, 상위 2바이트, 하위 2바이트의 정수에 접근할 때