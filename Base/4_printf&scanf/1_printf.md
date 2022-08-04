<h2> <strong> 1. printf </strong> </h2>

<h3> <strong> (1) 특수 문자 </strong> </h3>

|특수문자|의미|
|:---:|:---:|
|\\a|경고음|
|\\b|백스페이스|
|\\f|폼 피드 (프린터 출력을 위한 특수문자)|
|\\n|개행|
|\\r|캐리지 리턴|
|\\t|수평 탭|
|\\v|수직 탭 (프린터 출력을 위한 특수문자)|
|\\'|작은 따옴표 출력|
|\\"|큰 따옴표 출력|
|\\?|물음표 출력|
|\\ \\ |역슬래쉬 출력|

<h3> <strong> (2) 서식 문자 </strong> </h3>

|서식문자|자료형|출력 형태|
|:---:|:---:|:---:|
|%d|char, short, int|부호 있는 10진수 정수|
|%ld|long|부호 있는 10진수 정수|
|%lld|long long|부호 있는 10진수 정수|
|%u|unsigned int|부호 없는 10진수 정수|
|%o|unsigned int|부호 없는 8진수 정수|
|%x, %X|unsigned int|부호 없는 16진수 정수|
|%f|float, double|10진수 방식의 실수|
|%Lf|long double|10진수 방식의 실수|
|%e, %E|float, double|e, E 방식의 실수|
|%g, %G|float, double|값에 따라 %f 혹은 %e로 출력<br>(소숫점 이하자리가 늘어나면 %e로 출력)|
|%c|char, short, int|값에 대응하는 문자|
|%s|char *|문자열|
|%p|void *|포인터 주소 값|

서식 문자의 경우 아래의 방식을 사용해 정돈된 형식으로 출력할 수 있다.

* %8d: 필드 폭 8칸 확보, 오른쪽 정렬 후 출력
* %-8d: 필드 폭 8칸 확보, 왼쪽 정렬 후 출력