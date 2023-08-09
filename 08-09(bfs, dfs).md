# DFS 와 BFS
#### DFS
* DFS는 Depth-First-Search의 약어로 깊이 우선 탐색이라는 의미이다.
* 주로 트리와, 그래프 자료구조에서 이용이 된다.
#### DFS 특징
* 시작 노드에서부터 시작하여 멀리있는 노드까지 계속하여 노드를 탐색한다.
* 깊이 방향으로 탐색하다가 더 이상 갈 수 있는 노드가 없으면 이전 단계로 돌아가 다른 분기로의 탐색을 이어간다.
* 스택, 또는 재귀함수를 이용하여 구현할 수 있다.
#### DFS 예제
```
function dfs(node) {
  if (!visited[node]) {
    visited[node] = true;
    process.stdout.write(node + " ");  // 현재 노드 출력

    // 현재 노드와 연결된 인접 노드들을 재귀적으로 탐색
    for (const neighbor of graph[node]) {
      if (!visited[neighbor]) {
        dfs(neighbor);
      }
    }
  }
}
```
#### BFS
* Breadth-First_search의 약어로 너비 우선 탐색이라는 의미이다.
* 그래프에서 주로 이용된다.
#### BFS 특징
* 시작 노드에서부터 시작하여 인접한 모든 노드를 탐색한다.
* 같은 depth의 노드들을 먼저 탐색하고, 다음 depth의 노드들로 넘어간다.
* queue 자료구조를 이용하여 구현한다.
* 직관적이고 너비 우선 탐색하는 특성으로 인해 최단경로를 구할 때 유용하다.
#### DFS 예제
```
function bfs(startNode) {
  const queue = [startNode];
  visited[startNode] = true;

  while (queue.length > 0) {
    const node = queue.shift();
    process.stdout.write(node + " ");  // 현재 노드 출력

    for (const neighbor of graph[node]) {
      if (!visited[neighbor]) {
        queue.push(neighbor);
        visited[neighbor] = true;
      }
    }
  }
}
```
#### DP
* Dynamic Programming의 약어로 중복되는 부분 문제를 효율적으로 해결하는 알고리즘이다.
* 크게 topDown 방식과 bottomUp 방식이 있다.
#### DP Top-Down 방식 - 메모이제이션
* 중복된 계산을 방지하기 위해 계산한 결과를 저장하는 메모이제이션 기법을 활용한다.
```
function memoization(n, memo = {}) {
  if (n in memo) {
    return memo[n];
  }

  if (n <= 1) {
    return n;
  }

  memo[n] = memoization(n - 1, memo) + memoization(n - 2, memo);
  return memo[n];
}
```
#### DP Bottom-Up 방식 - 반복문 활용
* 작은 부분 문제부터 해결하며 결과를 누적시켜 큰 문제 해결하는 방식
```
function bottomUp(n) {
  if (n <= 1) {
    return n;
  }

  const dp = new Array(n + 1); // dp[i]: i번째 피보나치 수열 값
  dp[0] = 0;
  dp[1] = 1;

  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }

  return dp[n];
}
```
