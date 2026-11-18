# 보조자료
## 1. scnaf 및 보안
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>

void main(void) {
  char str[1000];
  printf("문장 입력: ");
  scanf("%[^\n]", str); // 엔터(\n) 전까지 공백 포함 문장 전체 입력

  // 문자열 끝에서부터 거꾸로 한 글자씩 출력
  for (int i = (int)strlen(str) - 1; i >= 0; i--) {
    printf("%c", str[i]);
  }
}
```

## 2. 함수의 포인터
```c
#include <stdio.h>
int add(int a, int b) {
  static int c;
  c = a + b;
  return &c;
}
void main() {
  int a = 11, b = 22;
  int *c;
  int* (*sum)(int, int) = add;
  c = sum(a, b);
  printf("%d\n", *c);
}
```

## 3. 2차원 배열
```c
#include <stdio.h>
void main() {
  int a[4][4] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16 };

  int i, j, s = 0;
  for (i = 0; i < 4; i++)
    for (j = 0; j < 4; j++)
      s += a[i][j];

  printf("%d\n", s);
}
```

## 4. 구조체로 2명의 3과목 성적을 생성해서 바이너리 형태로 my.bin에 저장해 줘
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
struct S {
  int k, e, m;
};
void main() {
  struct S a[3] = { {80, 90, 85}, {70, 75, 95}, {70, 75, 95} };
  FILE *p = fopen("my.bin", "wb");
  fwrite(a, sizeof(struct S), 3, p);
  fclose(p);
}
```

## 5. 이 파일을 읽고 개인 평균, 과목 평균을 출력해 줘
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
struct S {
  int k, e, m;
};
void main() {
  struct S a[3];
  FILE *p = fopen("my.bin", "rb");
  fread(a, sizeof(struct S), 3, p);
  fclose(p);
  printf("개인1: %.2f, 개인2: %.2f, 개인3: %.2f\n", (a[0].k + a[0].e + a[0].m) / 3.0, (a[1].k + a[1].e + a[1].m) / 3.0, (a[2].k + a[2].e + a[2].m) / 3.0);
  printf("과목1: %.2f, 과목2: %.2f, 과목3: %.2f\n", (a[0].k + a[1].k + a[2].k) / 3.0, (a[0].e + a[1].e + a[2].e) / 3.0, (a[0].m + a[1].m + a[2].m) / 3.0);
}
```

## 6. {2,4,1,5,3}을 버블 쇼팅해줘
```c
#include <stdio.h>

void main() {
  int a[] = { 2, 4, 1, 5, 3, 6, 5 }, i, j, t;
  for (i = 0; i < 6; i++)
    for (j = 0; j < 6 - i; j++)
      if (a[j] > a[j + 1]) {
        t = a[j];
        a[j] = a[j + 1];
        a[j + 1] = t;
      }
  for (i = 0; i < 7; i++)
    printf("%d ", a[i]);
}
```

# 퀴즈 2
## 7. 정수형 변수 2개에 각각 22와 33을 저장하고, 두 수의 합을 계산하여 화면에 출력하는 C언어 코드를 작성하시오.
```c
#include <stdio.h>

int main(void)
{
    int a = 22;
    int b = 33;
    int sum = a + b;

    printf("두 수의 합: %d\n", sum);

    return 0;
}
```
## 8. 명령행 인자(Command Line Arguments)로 두 정수를 입력받아 합을 출력하는 프로그램을 작성하시오.
```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[])
{
    int a = atoi(argv[1]);
    int b = atoi(argv[2]);

    printf("두 수의 합: %d\n", a + b);

    return 0;
}
```
## 9. 반복문(for 또는 while)을 사용하여 5부터 10까지의 정수를 모두 더한 결과를 화면에 출력하는 C언어 코드를 작성하시오.
```c
#include <stdio.h>

int main(void)
{
    int sum = 0;

    for (int i = 5; i <= 10; i++) {
        sum += i;
    }

    printf("%d\n", sum);

    return 0;
}
```
## 10. 동적 메모리 할당(malloc)을 활용하여 정수 3개 공간을 할당받은 뒤, {11, 33, 55}를 저장하고 이들의 합을 출력(해제 포함)하는 C언어 코드를 작성하시오.
```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int *arr = (int *)malloc(3 * sizeof(int));

    arr[0] = 11;
    arr[1] = 33;
    arr[2] = 55;

    int sum = arr[0] + arr[1] + arr[2];

    printf("%d\n", sum);

    free(arr);

    return 0;
}
```
## 11. 다음 3명의 성적(국어 kr, 영어 en)을 구조체로 초기화하고 개인별 평균을 구하시오. 대상:J.C. Shim, G.D. Hong, J.Y. Ko 
```c
#include <stdio.h>

struct Student {
    char name[20];
    int kr;
    int en;
};

int main(void)
{
    struct Student students[3] = {
        {"J.C. Shim", 90, 85},
        {"G.D. Hong", 80, 95},
        {"J.Y. Ko",  75, 90}
    };

    for (int i = 0; i < 3; i++) {
        double avg = (students[i].kr + students[i].en) / 2.0;

        printf("이름: %s\n", students[i].name);
        printf("국어: %d, 영어: %d\n",
               students[i].kr, students[i].en);
        printf("평균: %.2f\n\n", avg);
    }

    return 0;
}
```
