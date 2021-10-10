# 모든 순열

## 문제 1
N이 주어졌을 때, 1부터 N까지의 수로 이루어진 순열을 사전순으로 출력하는 프로그램을 작성하시오.

## 입력
첫째 줄에 N(1 ≤ N ≤ 8)이 주어진다. 

## 출력
첫째 줄부터 N!개의 줄에 걸쳐서 모든 순열을 사전순으로 출력한다.

## 풀이
```python
from itertools import permutations #순열 함수

N = int(input())
N_list = [i for i in range(1, N+1)]

for numbers in list(permutations(N_list)):
    for num in numbers:
        print(num, end=' ')
    print()


```


## 문제 2
N개의 정수로 이루어진 배열 A가 주어진다. 이때, 배열에 들어있는 정수의 순서를 적절히 바꿔서 다음 식의 최댓값을 구하는 프로그램을 작성하시오.

|A[0] - A[1]| + |A[1] - A[2]| + ... + |A[N-2] - A[N-1]|

## 입력
첫째 줄에 N (3 ≤ N ≤ 8)이 주어진다. 둘째 줄에는 배열 A에 들어있는 정수가 주어진다. 배열에 들어있는 정수는 -100보다 크거나 같고, 100보다 작거나 같다.

## 출력
첫째 줄에 배열에 들어있는 수의 순서를 적절히 바꿔서 얻을 수 있는 식의 최댓값을 출력한다.

## 풀이

```python

from itertools import permutations  #순열 함수
import sys
 
# 주어진 값 입력
x = int(sys.stdin.readline())
y = list(map(int, sys.stdin.readline().split()))
 
# permutation 저장(per: reference of permutation tuples)
per = permutations(y)
ans = 0
 
# 순열마다 차이를 더해(s), ans 보다 크면 ans를 update
for i in per:
    s = 0
    for j in range(len(i)-1):
        s += abs(i[j]-i[j+1])
    if s > ans:
        ans = s
 
print(ans)


```
