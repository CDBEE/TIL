# DFS(Depth-First Search, 깊이 우선 탐색)

Date: October 11, 2021

# DFS(Depth-First Search, 깊이우선탐색)

: 트리나 그래프를 탐색하는 방법 중 하나로 정점을 우선으로 탐색하는 방법

1. 깊이 우선 탐색을 사용하는 경우
- 분기를 완벽하게 탐색하고 싶을때 사용한다.
1. 깊이 우선 탐색의 특징
- 재귀, 비재귀적 구현 둘 다 가능하다.
- 무한한 길이 있을 경우에도 탐색이 가능하다.
- 알고리즘 구현(비재귀적)에 Stack이 필요하다.
- BFS에 좀 느리다.

![](https://ww.namu.la/s/1fe9246903b78fae07577b243a0b22791e02cb39640d5cbaae10d9849343b4ea6f162a9a677a5892fbf7819abd4ef7221ebd3608849cfb66793411fb5e643951cb17465521d04a2636502ad7d7edb0767aa339b522241b54d0543ab00ca52950)

3.재귀적 구현(인접리스트)

```java
void dfs(LinkedList<Integer>[] list, boolean[] visited, int idx){
	visit[idx] = true;
	Iterator<Integer> it = list.get(idx).listIterator();
	while(it.hasNext()){
		int n = it.next();
		if(!visited[n]) dfs(list, visited, n);
	}
}
```

3. 비재귀적 구현(행렬)

```java
void dfs(int[][] board, boolean[] visited, int idx){
	Stack<Integer> st = new Stack<>();
	st.push(idx);
	visited[idx] = true;
	while(!st.isEmpty()){
		int N = st.pop();
		for(int i=0;  i < board.length; i++){
			if(board[N][i] == 1 && !visited[i]){
				st.push(i);
				visited[i] = true;
			}
		}
	}	
}
```

1. 너비 우선 탐색의 과정
    1. stack에 루트 노드 혹은 시작점을 넣는다.
    2. 해당 노드를 방문처리한다.
    3. Stack이 비어있지 않는 동안 while문 루프
    4. Stack에서 하나를 빼서 해당 노드와 연결된 노드들을 다 Stack에 add한다.
    5. Stack에서 pop할 경우 가장 LIFO이기 때문에 마지막에 넣은 것을 빼서 탐색
    6. → 정점까지 방문하게 된다.