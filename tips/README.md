# 팁 공유

## 공통

### 적어도 한 번쯤은 봐야할 것

- [BOJ 작동 원리 및 기타 질문](https://www.acmicpc.net/blog/view/55)
- [BOJ 자주 묻는 질문 (채점/소스 등)](https://www.acmicpc.net/help/faq)
- [BOJ 자주 틀리는 요인 정리](https://www.acmicpc.net/blog/view/70)
- [어떤 버전의 C/C++/Java/Python 을 써야할까? (대표 채점 환경)](https://www.acmicpc.net/blog/view/95)

## C++

### 빠른 입출력

- 후술되는 내용은 cin, cout을 사용할 때의 얘기입니다. C-style처럼 scanf/printf로 입출력을 하실거라면 그냥 쓰시면 됩니다. 걔네는 충분히 빠릅니다.
- 'endl'은 개행 + 출력 버퍼 비우기입니다. OJ에서 화면에 바로 출력되는 지의 여부는 중요하지 않기 때문에 가급적이면 개행만 하는 '\n'을 사용하시는 게 속도 향상에 좋습니다.
- 다음 함수들을 사용하는 것도 좋습니다.

```cpp
ios_base::sync_with_stdio(false);
// C와 C++ 버퍼 분리.
// 단 cin과 scanf/getchar 등을 같이 사용할 수 없고,
// cout과 printf/putchar 등을 같이 사용할 수 없다.

cin.tie(nullptr);
cout.tie(nullptr);
// 각각 cin/cout의 묶음을 분리함
// 가급적 NULL보다 nullptr를 활용하는 습관을 들이자.
```

### 하나의 헤더로 모든 헤더를 포함하자!

```cpp
#include <bits/stdc++.h>
```

- 해당 헤더는 C++ STL의 대부분의 헤더 (Algorithm, Vector, Utility 등...)들이 포함되어 있습니다.
- 보통 코딩 사이트/코딩 테스트에서 코딩할때 많이 사용하는 헤더입니다. 코딩에 필요한 대부분의 헤더들이 포함되어 있으므로, 시간이 촉박한 코딩 테스트에서 일일히 필요한 헤더를 생각하고 넣는데 들여야 하는 시간을 아낄 수 있습니다.
- 하지만 불필요하게 많은 헤더들이 들어가기 때문에, 프로그램이 무거워지고, 컴파일 시간도 많이 잡아먹습니다. 따라서 코딩 테스트와 같은 제한적인 상황에서만 사용하는 것이 좋습니다.
- GCC 컴파일러에 내장되어 있는 헤더이므로, 해당 컴파일러를 지원하는 백준, 코드포스 등에서 유용하게 사용할 수 있습니다. Visual Studio 같은 IDE에는 없으니 직접 헤더를 추가해야 합니다.

## Python3

### 입력받기

때로는 input() 함수를 사용하면 동작 속도가 느려서 시간 초과로 오답 판정을 받을 수 있습니다. 이때는 아래와같은 입력함수를 사용하거나 `python3` 컴파일러를 `pypy` 로(또는 반대로) 변경해볼 수 있습니다.

```python
import sys
input_data = sys.stdin.readline().rstrip() # rstrip(): 줄 끝 개행문자 삭제
print(input_data)
```

```python
from sys import stdin
input = stdin.readline
n = int(input())
print(n)
```

### 선언하기

- 1차원 배열

```python
arr = [0 for _ in range(n)]
```

- 2차원 배열

```python
arr = [ [0 for _ in range(cols)] for _ in range(rows)]
```

### 출력하기

- 줄바꿈 없이 출력

```python
print('Hello', end = '')
```

- 특정 기호를 사이사이에 두고 출력

```python
print(','.join('Hello'))
```

### Count

```python
# python list 의 count() 함수를 사용하면 시간 초과가 날 수 있습니다.
n_list = [1, 9, 8, 8, 5, 1, 8]

cnt_list = []
for n in list(set(n_list)):
	cnt_list.append([n, n_list.count()])
```

```python
# Counter 를 사용하세요!
from collections import Counter

n_list = [1, 9, 8, 8, 5, 1, 8]
cnt_list = Counter(n_list).most_common()
```

### 재귀함수

- 재귀함수를 사용하는 경우 맨 위에 이렇게 limit 을 정해줘야 합니다.
- 그렇지 않으면 `런타임 에러 (RecursionError)` 가 뜹니다…

```python
import sys
sys.setrecursionlimit(10000)
```

### 내장함수 접근시간

제한 시간 달성하기 위해 참고하시면 좋을 것 같습니다.

[파이썬 기본 연산자들의 시간 복잡도(Big-O) 정리](https://dev.plusblog.co.kr/42)

### 입력 함수를 이용하여 테스트 케이스 받기

- 2953번

`open()` 함수를 이용하여 만든 파일 객체를 `sys.stdin` 에 대입하고,

`input()` 대신 `sys.stdin.readline()` 을 사용합니다.

```python
import sys
sys.stdin = open('input.txt', 'r')

scores_sum=[]
for i in range(5):
    scores_sum.append(sum(list(map(int,sys.stdin.readline().split()))))
print(scores_sum.index(max(scores_sum))+1,max(scores_sum))
```

잘 풀었다면 `sys.stdin = open('input.txt', 'r')` 를 지우고 제출하면 됩니다. (저는 주석처리를 합니다.)

> 지우지 않고 제출할 시, `런타임 에러` 가 뜹니다.

```python
import sys

scores_sum=[]
for i in range(5):
    scores_sum.append(sum(list(map(int,sys.stdin.readline().split()))))
print(scores_sum.index(max(scores_sum))+1,max(scores_sum))
```