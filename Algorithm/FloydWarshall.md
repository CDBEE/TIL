# Floyd-Warshall Algorithm

Date: October 13, 2021

# 플로이드-워셜 알고리즘

## 플로이드 워셜 알고리즘이란?

- 그래프에서 모든 정점에서 모든 정점으로의 최단거리를 탐색할 때 사용하는 알고리즘.
- 거쳐가는 정점을 기준으로 최단거리를 구하는 것을 핵심 아이디어로 삼는다.
- 말이 어렵지만 해당 노드를 향해 거쳐가면서 테이블을 새로 갱신하는 것이다.
- 다익스트라 알고리즘에서는 음수 가중치의 간선을 계산하지 못하지만 플로이드 워셜 알고리즘은 가능하다.

![https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/Floyd-Warshall_example.svg/1280px-Floyd-Warshall_example.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/Floyd-Warshall_example.svg/1280px-Floyd-Warshall_example.svg.png)

출처 : 위키백과, 플로이드-워셜 알고리즘

[플로이드-워셜 알고리즘 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%ED%94%8C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%9B%8C%EC%85%9C_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)

## 플로이드 워셜 알고리즘 자바 코드

```java
int[][] board; // 그래프

for(int k=0; k < board.length; k++){ //중간 노드
	for(int i=0; i < board.length; i++){ //시작 노드
		for(int j=0; j < board.length; j++){ //도착 노드
			if(board[i][j] > board[i][k] + board[k][j]){
				board[i][j] = board[i][k] + board[k][j];
			}
		}
	}
}
```

### 플로이드 워셜 알고리즘의 복잡도

- 시간 복잡도의 경우 $o(n^3)$, 공간 복잡도의 경우 $o(n^2)$이다.