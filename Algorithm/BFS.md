# BFS(Breadth-First Search, 너비우선탐색)

Date: October 9, 2021

# BFS(Breadth-First Search, 너비우선탐색)

: 트리나 그래프를 탐색하는 방법 중 하나로 인접한 노드들을 먼저 탐색하는 방법

1. 너비 우선 탐색을 사용하는 경우
- 최단 경로를 탐색할 경우 사용한다.
- 임의의 경로를 찾고 싶을때 사용한다.
1. 너비 우선 탐색의 특징
- 재귀적으로 동작하지 않음
- 무한한 길이 있을 경우에도 탐색이 가능하다.
- 알고리즘 구현에 Queue가 필요하다.
- 시간복잡도
    - 인접리스트 : O(N + E)
    - 인접행렬 : O(N^2)

![](https://ww.namu.la/s/1fe9246903b78fae07577b243a0b22791e02cb39640d5cbaae10d9849343b4ea6f162a9a677a5892fbf7819abd4ef7221ebd3608849cfb66793411fb5e643951cb17465521d04a2636502ad7d7edb0767aa339b522241b54d0543ab00ca52950)

1. 구현(행렬)

```java
void bfs(int[][] board, boolean[] visited, int idx){
	Queue<Integer> q = new LinkedList<>();
	q.add(idx);
	visited[idx] = true;
	while(!q.isEmpty()){
		idx = q.poll();
		for(int i=0; i < board.length(); i++){
			if(board[idx][i] != 0 && !visited[i]){
				q.add(i);
				visited[i] = true;
			}
		}
	}
}
```

3.구현(인접리스트)

```java
void bfs(LinkedList<Integer>[] list, boolean[] visited, int idx){
	Queue<Integer> queue = new LinkedList<>();
	queue.add(idx);
	visited[idx] = true;
	while(!q.isEmpty()){
		idx = q.poll();
		Iterator<Integer> it = list[idx].listIterator();
		while(it.hasNext()){
			int i = it.next();
			visited[i] = true;
			queue.add(i);
		}
	}
}
```

1. 너비 우선 탐색의 과정
    1. Queue에 루트 노드 혹은 시작점을 넣는다.
    2. 해당 노드를 방문처리한다.
    3. Queue가 비어있지 않는 동안 while문 루프
    4. Queue에서 하나를 뺀다.
    5. 노드 혹은 행렬을 돌면서 인접 노드들을 Queue에 넣고 방문처리한다.


참고
- [BFS이미지](https://namu.wiki/w/%EB%84%88%EB%B9%84%20%EC%9A%B0%EC%84%A0%20%ED%83%90%EC%83%89?from=%EB%84%93%EC%9D%B4%20%EC%9A%B0%EC%84%A0%20%ED%83%90%EC%83%89)
- [[알고리즘] 너비 우선 탐색이란 (BFS)](https://gmlwjd9405.github.io/2018/08/15/algorithm-bfs.html)