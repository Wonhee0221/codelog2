## 문제 1
 그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오.  
단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고,  
더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.

조건: 첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다.  
다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다.  
어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.  
첫째 줄에 DFS를 수행한 결과를, 그 다음 줄에는 BFS를 수행한 결과를 출력한다. V부터 방문된 점을 순서대로 출력하면 된다.

문제풀이 (파이썬)  
``` python
n,m,v = map(int,input().split())
graph = [[0]*(n+1) for _ in range(n+1)]
for i in range(n+1):
    a,b = map(int,input().split())
    graph[a][b] = graph[b][a] = 1

# DFS구현
visited_dfs = [0]*(n+1)
def dfs(v):
    visited_dfs[v] = 1                         # 방문처리
    print(v,end=' ')                         
    for i in range(n+1):
        if visited_dfs[i]==0 and graph[i][v]:  # 방문했었는지, 그리고 간선이 있는지 확인
        dfs(i)                                 # 재귀함수 호출
dfs(v)

# BFS구현
visited_bfs = [0] * (n+1)
from collections import deque
def bfs(v):
    visited_bfs[v] = 1                         # 방문처리
    queue = deque()
    queue.append(v)                            # 큐에 노드 삽입
    while queue:                               # 큐에 노드가 없을때까지 반복
        node = queue.popleft()                 # 큐에서 빼주기
        print(node,end=' ')
        for i in range(n+1):
            if visited_bfs[i] == 0 and graph[i][node]: # 방문했었는지, 그리고 간선이 있는지 확인
                queue.append(i)                        # 큐에 노드 삽입
                visited_bfs[i] = 1                     # 방문처리
print()
bfs(v)
```

## 문제 2  
![문제 2](https://user-images.githubusercontent.com/91041488/139573315-490b5020-3ed2-497e-9dcf-ef32c3605ce9.jpg)  

문제풀이 (파이썬)  -최소의 칸수를 구하는 프로그램이기 때문에 BFS를 사용한다.
``` python
from sys import stdin
N, M = map(int, stdin.readline().split())
# matrix 배열
matrix = [stdin.readline().rstrip() for _ in range(N)]
# 방문경로 배열
visited = [[0]*M for _ in range(N)]
# 좌/우/위/아래 방향 이동
dx, dy = [-1, 1, 0, 0], [0, 0, -1, 1]

# BFS 경로 탐색
# queue 방식 사용
queue = [(0,0)]
visited[0][0] = 1

while queue:
    x, y = queue.pop(0)

    if x == N-1 and y == M-1:
        # 최종 경로 도착
        print(visited[x][y])
        break

    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        if 0 <= nx < N and 0 <= ny < M:
            if visited[nx][ny] == 0 and matrix[nx][ny] == '1':
                visited[nx][ny] = visited[x][y] + 1
                queue.append((nx,ny))
```
## 문제 3  
![문제 3](https://user-images.githubusercontent.com/91041488/139573393-e6f8de0c-34ee-4de1-bb49-289acaa85159.jpg)  
문제풀이 (파이썬)  -DFS로 푼다.
``` python
import sys
sys.setrecursionlimit(100000)

# T개의 테스트를 풀어야 하므로 T번 수행한다.
T = int(input())
for _ in range(T):
    # 순열의 길이 N과 순열을 받아서 graph를 만든다.
    N = int(input())
    permutation = list(map(int, input().split(" ")))

    graph = {n + 1 : [permutation[n]] for n in range(N)}

    # dfs로 탐색하여 진행경로(trace)상에 있는 노드중에 한번 방문한 노드가 있다면
    # 순환구조로 판별하고 return한다. 진행경로는 갈림길마다 하나씩 reset 하므로
    # 해당 노드의 모든 갈래길을 다 탐색한 후에는 해당 노드를 지워주어야 한다.
    # 또 한번 탐색된 노드는 다시 방문했을때 순환구조가 중복 count 될 수 있으므로
    # 진행경로 추적을 위한 set 말고 방문 기록을 남기기 위한 set을
    # 추가적으로 만들어서 기록한다. 그리고 trace를 통해 순환 구조가 발견되면
    # count를 하나 증가시키면서 탐색을 마치고 visited에 의해 탐색이 마쳐질 경우는
    # count를 올리지 않아야 한다.

    visited = set()
    cicle_count = [0]
    def dfs(v, trace = set()):
        if v in trace:
            cicle_count[0] += 1
            return

        if v in visited:
            return

        visited.add(v)
        trace.add(v)
        for w in graph[v]:
            dfs(w, trace)
        trace.remove(v)

    for v in list(graph):
        dfs(v)

    print(cicle_count[0])
```
## 문제 4 
![문제 4](https://user-images.githubusercontent.com/91041488/139575252-8018de44-b0a4-49ae-9042-9c9358aa0e0e.jpg)  
``` python
import sys
input = sys.stdin.readline
from collections import deque
 
def bfs(graph, start, visited):
    queue = deque([start])
 
    while queue:
        v = queue.popleft()
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i] = True
 
 
n, m = map(int, input().split())
 
graph = [[] for _ in range(n+1)]
 
for i in range(m):
    a , b = map(int, input().split())
    graph[a].append(b)
    graph[b].append(a)
    graph[a].sort()
    graph[b].sort()
 
visited = [False] * (n+ 1)
 
ans = 0
for i in range(1, n+1):
    if visited[i] == False:
        bfs(graph, i, visited)
        ans += 1
 
print(ans)
```
# 문제 5
![문제 5](https://user-images.githubusercontent.com/91041488/139576308-56bd8a86-c705-469e-acd6-6f82b5c50013.jpg)  
``` python
from sys import stdin
n = int(input())
# 데이터 저장용 공간 matrix
matrix = [[0]*n for _ in range(n)]
# 방문 내역 저장용 visited
visited = [[0]*n for _ in range(n)]

# matrix에 아파트 유무 0과 1 저장
for i in range(n):
    line = stdin.readline().strip()
    for j, b in enumerate(line):
        matrix[i][j] = int(b)

# 방향 확인용 좌표 dx와 dy
# 중앙을 기준으로 좌/우/위/아래
dx = [-1, 1, 0, 0]
dy = [0, 0, 1, -1]

# DFS 함수 정의
def dfs(x, y, c):
    visited[x][y] = 1   # 방문 여부 표시
    global nums            # 아파트 단지 수를 세기위한 변수
    # 아파트가 있으면 숫자를 세어줍니다.
    if matrix[x][y] == 1:
        #matrix[x][y] = c # 아파트 단지별 숫자 표시용
        nums += 1
    # 해당 위치에서 좌/우/위/아래 방향의 좌표를 확인해서 dfs 적용
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        if 0 <= nx < n and 0 <= ny < n:
            if visited[nx][ny] == 0 and matrix[nx][ny] == 1:
                dfs(nx,ny, c)

cnt = 1 # 아파트 단지 세기 위한
numlist = [] # 아파트 단지별 숫자
nums=0 # 아파트 수
for a in range(n):
    for b in range(n):
        if matrix[a][b] == 1 and visited[a][b] == 0:
            dfs(a,b,cnt)
            numlist.append(nums)
            nums = 0
#            cnt += 1 # 아파트 단지 별 표시용

print(len(numlist))
for n in sorted(numlist):
    print(n)
    
 ```
