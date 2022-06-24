---
layout: post
title:  "ModernC:1.GettingStarted"
date:   2022-06-24-14-00
categories: 컴퓨터_과학, ModernC
---
## 1.1. Imperative Programming

> 0.1.1.1. C는 명령형 프로그래밍 언어다.

여기서 명령형 프로그래밍 언어(imperative programming language)란 인간과 컴퓨터 간의 소통에 있어 인간이 "명령/질서"(order)을/를 부여하도록 하는 언어를 뜻한다. C언어가 일례다. Jen Gustedt에 따르면 *Modern C*는 C언어만이 아니라 C언어 방언(jargon)까지 익힐 수 있는 교재다. C언어 방언은 $$\textrm{jargon}^C$$와 같이 표기된다. 아래 C코드를 $$\textrm{jargon}^C$$로 읽어 보자.

```c
// getting-started.c
#include <stdlib.h>
#include <stdio.h>

/* The main thing that this program does */
int main(void){
    // Declarations
    double A[5] = {
        [0] = 9.0,
        [1] = 2.9,
        [4] = 3.E+25,
        [3] = .0007,
    };

    // Doing some work
    for (size_t i = 0; i < 5; i++) {
        printf("element_%zu_is_%g,_\tits_square_is_%g\n",
               i,
               A[i],
               A[i]*A[i]);
    }

    return EXIT_SUCCESS;
}
```
```
C:\ModernC>getting-started
element_0_is_9,_        its_square_is_81
element_1_is_2.9,_      its_square_is_8.41
element_2_is_0,_        its_square_is_0
element_3_is_0.0007,_   its_square_is_4.9e-007
element_4_is_3e+025,_   its_square_is_9e+050
```
이 프로그램은 큰따옴표(`"`)로 묶인 부분을 $$\textrm{출력print}^C$$한다. `getting-started.c` 프로그램의 실질적인 작업은 이 부분이 시작되는 라인에서 이 부분이 시작되는 라인의 `printf`의 `()`가 끝나는 라인까지 이루어진다. C는 이와 같은 간격을 $$\textrm{문장statement}^C$$이라고 부른다. 또 이 특정한 문장은, `printf`라고 명명된 $$\textrm{함수function}^C$$에 대한 하나의 $$\textrm{호출call}^C$$이다.
```c
		printf("element_%zu_is_%g,_\tits_square_is_%g\n",
               i,
               A[i],
               A[i]*A[i]);
```
여기서 `printf` 함수는 한 쌍의 $$\textrm{괄호parantheses}^C$$로 묶인 네 개의 $$\textrm{전달인자arguments}^C$$를 받는다.

## 1.2. Compiling and Running
>**0.1.2.1.** C는 컴파일 프로그래밍 언어다. 

**컴파일러**(compiler)란 내가 작성한 C 텍스트를 기계가 이해할 수 있는 $$\textrm{이진 코드binary code}^C$$
나 $$\textrm{실행 파일executable}^C$$로 번역하는 특수한 프로그램을 말한다. 컴파일러의 이름과 명령행 인자(command-line arguments)는 프로그램을 실행하게 될 $$\textrm{플랫폼platform}^C$$에 크게 의존한다. 여기에는 단순한 이유가 있다. 대상 이진 코드는 $$\textrm{플랫폼 종속적platform dependent}^C$$이다. 이는 C의 존재 이유 가운데 하나다. C는 (주로 $$\textrm{어셈블러assembler}^C$$라고 부르는) 여러 상이한 장치 특정적 언어에 대해 추상화를 제공한다.  

>**0.1.2.2.** 올바른 C 프로그램은 상이한 플랫폼 간에 이식성을 지닌다.

저자는 이식성(portability)을 보장하는 "올바른" C프로그램 작성법을 보이는 데 많은 공을 들일 생각이라고 한다. 다만 불행히도 스스로 "C"라고 주장하지만 근래의 표준을 보장하지 않는 플랫폼이 존재한다고 한다. 또한 올바르지 않은 프로그램을 허용하는 보장된 플랫폼이 존재한다고 한다. 따라서 단일 플랫폼에서 하나의 프로그램을 실행 및 테스팅하는 작업이 항상 이식성을 보증하지는 않는다고 한다. 기본적으로는 컴파일러의 책무인데, 만약 (Linux나 macOS와 같은) POSIX 시스템을 지닌다면 `c99` 라는 이름의 C 컴파일러를 지닐 가능성이 높다. 그런데 내 맥북 에어는 잠든지 오래이므로 `gcc`를 사용하도록 한다. 명령 프롬프트에 다음처럼 입력한다.
```
C:\ModernC>gcc -std=c99 -Wall -lm -o getting-started getting-started.c
```
여기서
- `c99`는 컴파일러 프로그램을 말한다.
- `-Wall`은 비일반적인 것이 발견되면 경고를 달라는 것이다.
- `-o getting-started`는 `getting-started`라는 이름의 파일에 $$\textrm{컴파일러 출력compiler output}^C$$을 저장하라는 것이다.
- `getting-started.c`는 $$\textrm{소스 파일source file}^C$$을 명명한다. 
- `-lm`은 필요하다면 표준 수학 함수를 포함하라는 것이다. 이에 관해서는 나중에 다룬다.

그런 다음 다음처럼 입력한다. 이는 새롭게 생성된 $$\textrm{실행 파일executable}^C$$을 $$\textrm{실행execute}^C$$하는 것이다.
```
C:\ModernC>getting-started
```
그렇다면 1.1. Imperative Programming에서 본 것과 똑같은 결과를 관찰할 수 있을 것이다. 이것이 **이식성**(portable)의 뜻이다. 프로그램을 어디서 실행하든, 그 $$\textrm{행동behavior}^C$$은 동일해야 한다. 이를 위해서는 컴파일러가 생성하는 $$\textrm{진단적 출력diagonstic output}^C$$ 또는 경고에 주의해야 한다.

>**0.1.2.3.** C 프로그램은 경고 없이 깔끔하게 컴파일되어야 한다.