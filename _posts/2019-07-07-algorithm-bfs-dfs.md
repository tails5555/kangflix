---
layout: post
title: "BFS 와 DFS"
date: 2019-07-09 15:00:00 +09:00
image: "/assets/img/category/ct_algorithm.png"
category: 'algorithm'
tags:
- Algorithm
- BFS
- DFS
description: BFS 와 DFS 에 대해 알아봅니다.
introduction: BFS 와 DFS 에 대해 알아봅니다.
---

# Thinking

트리(Tree) 를 순회하는 방법은 3 가지로 나뉩니다.

- 전위 순회(Pre-Order)
- 중위 순회(In-Order)
- 후위 순회(Post-Order)

트리의 Node 들은 계층이 정해져 있어 `visited` 배열이 없어도 충분히 순회가 가능합니다.

애초에 트리(Tree) 는 노드의 개수가 N 개이면, (N - 1) 개의 간선들로 이뤄지고, 순환이란 것 자체가 없어야 합니다.

그렇지만 그래프의 정점들은 계층이 따로 정해진 것도 아니기 때문에 어느 지점에서 시작을 하든 순회 결과 값은 달라질 수 있습니다.

(물론 정점들의 가중치 순서를 기준으로 ASC 를 하는 것이 관례이긴 합니다.)

그래서 이번 문서에서는 그래프의 탐색 방법인 DFS 와 BFS 를 다뤄보도록 하겠습니다.

## Adjacency Matrix vs List

그래프 탐색 알고리즘을 공부하기 앞서 인접 행렬(Adjacency Matrix), 인접 리스트(Adjacency List) 둘 중 하나를 선택해야 하는 경우가 있습니다.

**인접 행렬을 사용하는 경우**

- 그래프 간 연결 여부 확인은 시간 복잡도가 O(1) 정도 소모되어 쉽게 확인할 수 있습니다.
- 쓸모 없는 메모리 낭비가 나옵니다. (희소 행렬을 만들 수도 있습니다.)
- 탐색 속도도 O(V^2) 로 나오게 됩니다.
- 대부분 알고리즘 저지 문제에선 행렬보다 인접 리스트를 사용하는 것을 권장.
- 단, Froyd-Warshall 알고리즘을 사용하면 이를 사용할 수 밖에 없습니다.

**인접 리스트를 사용하는 경우**

- 희소 행렬에 대한 메모리 낭비를 더 크게 줄입니다.
- 탐색 속도는 O(V + E) 로 더욱 향상 시킬 수 있습니다.
- 그래프 간 연결 여부 확인은 O(E) 정도 소모되어 이런 점에선 치명적입니다.
- 대부분 그래프 알고리즘은 이를 사용하여 구현합니다.
- 리스트 대신에 Set 를 사용하면 그래프 연결 확인을 좀 더 개선할 수 있습니다.

## DFS

- Depth 1st Search. 깊이 우선 탐색.
- 정점들의 가중치 순서를 중점으로 탐색하는 방법입니다.
- Stack 이나 Recursive (재귀 함수) 를 사용하여 구현할 수 있습니다. (개인적으론 재귀 함수를 사용하는 것을 추천.)
- 대형 마트에 왔을 때 가장 신선한 1++ 등급 한우를 우선으로 찾아 구매하는 것과 유사합니다.
- 시간 복잡도는 O(V + E). 공간 복잡도는 O(V).
- 퇴각 검색(Backtracking, 백트래킹) 을 사용할 때 이와 비슷한 메커니즘을 발견할 수 있습니다.
- 트리를 DFS 로 순회하면 Pre-Order (전위 순회) 한 결과랑 똑같은 순서가 나오지만, 결국엔 Pre-Order 가 더 빠릅니다.

소스 코드는 다음과 같습니다.

**재귀 함수를 사용하는 방법**

```java
import java.util.Arrays;
import java.util.List;

public class DFS_Recursive {
    static final int N = 7;
    static final int S = 1;

    static List<Integer>[] graph = new List[] {
        null,
        Arrays.asList(2, 5),
        Arrays.asList(1, 4, 7),
        Arrays.asList(5, 6, 7),
        Arrays.asList(2, 7),
        Arrays.asList(1, 3),
        Arrays.asList(3, 7),
        Arrays.asList(2, 3, 4, 6)
    };

    static boolean[] visited;
    static StringBuilder sb;

    static void dfs_recursive(int vtx){
        visited[vtx] = true;
        sb.append(String.format("%d ", vtx));
        for(int next : graph[vtx]){
            if(!visited[next]){
                dfs_recursive(next);
            }
        }
    }

    static void initialize(){
        visited = new boolean[N + 1];
        sb = new StringBuilder();
    }

    public static void main(String[] args){
        initialize();
        dfs_recursive(S);
        System.out.println(sb.toString());
    }
}
```

**Stack 자료구조를 사용하는 방법**

DFS 의 순서를 올바르게 얻기 위해 인접 리스트 순서를 거꾸로 작성해야 합니다.

그래서 Stack 자료구조로 DFS 를 구현하는 것을 비추천 하는 것입니다.

```java
import java.util.Arrays;
import java.util.List;
import java.util.Stack;

public class DFS_Stack {
    static final int N = 7;
    static final int S = 1;

    static List<Integer>[] graph = new List[] {
        null,
        Arrays.asList(5, 2),
        Arrays.asList(7, 4, 1),
        Arrays.asList(7, 6, 5),
        Arrays.asList(7, 2),
        Arrays.asList(3, 1),
        Arrays.asList(7, 3),
        Arrays.asList(6, 4, 3, 2)
    };

    static void dfs_stack(){
        boolean[] visited = new boolean[N + 1];

        Stack<Integer> stack = new Stack<>();
        stack.push(S);

        StringBuilder sb = new StringBuilder();
        while(!stack.isEmpty()){
            int cur = stack.pop();
            if(!visited[cur]) {
                sb.append(String.format("%d ", cur));
                visited[cur] = true;
                for (int next : graph[cur]) {
                    if (!visited[next]) {
                        stack.push(next);
                    }
                }
            }
        }

        System.out.println(sb.toString());
    }

    public static void main(String[] args){
        dfs_stack();
    }
}
```

## BFS

- Breadth 1st Search. 너비 우선 탐색.
- 정점을 방문한 이후 다음 정점들의 또 다른 정점들을 탐색하는 방법입니다.
- Queue 를 사용하여 구현할 수 있습니다.
- 대형 마트에 왔을 때 무난하게 먹을 수 있는 소고기들을 직접 찾아서 구매하는 것과 유사합니다.
- 시간 복잡도는 O(V + E). 공간 복잡도는 O(V).
- 대신 DFS 보다 탐색으로 인한 메모리 요구량이 많아지는 단점이 있습니다.
- 트리를 BFS 로 탐색하면, Level Order 를 이루게 됩니다.

소스 코드는 다음과 같습니다.

```java
import java.util.Arrays;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

public class BFS {
    static final int N = 7;
    static final int S = 1;

    static List<Integer>[] graph = new List[] {
        null,
        Arrays.asList(2, 5),
        Arrays.asList(1, 4, 7),
        Arrays.asList(5, 6, 7),
        Arrays.asList(2, 7),
        Arrays.asList(1, 3),
        Arrays.asList(3, 7),
        Arrays.asList(2, 3, 4, 6)
    };

    static void bfs(){
        Queue<Integer> queue = new LinkedList<>();
        boolean[] visited = new boolean[N + 1];

        queue.offer(S);
        visited[S] = true;

        StringBuilder sb = new StringBuilder();
        while(!queue.isEmpty()){
            int cur = queue.poll();
            sb.append(String.format("%d ", cur));
            for(int next : graph[cur]) {
                if(!visited[next]){
                    queue.offer(next);
                    visited[next] = true;
                }
            }
        }

        System.out.println(sb.toString());
    }

    public static void main(String[] args){
        bfs();
    }
}
```