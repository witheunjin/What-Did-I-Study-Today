# 2020.07.28.Tue

**📚공부한 거 List**📚

- 종만북 - 그래프의 깊이 우선 탐색 (간선)
- 종만북 - 그래프의 너비 우선 탐색
- 종만북 - 최단 경로 알고리즘

-----

## 🌞[종만북] 그래프의 깊이 우선 탐색🌞

### 🌴 간선의 분류 🌴

**그래프의 깊이 우선 탐색 스패닝 트리** (혹은 **DFS Spanning Tree**)를 생성하고 나면 그래프의 간선을 다음과 같이 분류할 수 있다.

#### 🌱 트리 간선(Tree Edge)

스패닝 트리에 포함된 간선

#### 🌱 순방향 간선(Forward Edge)

선조에서 자손으로 연결되지만, 트리 간선이 아닌 간선(중간노드를 거치는 다른 경로가 있으면 안됨)

#### 🌱역방향 간선(Back Edge)

자손에서 선조로 연결되는 간선

#### 🌱 교차 간선(Cross Edge)

선조와 자손 관계가 아닌 정점들 간에 연결된 간선

-----

#### 🌱 무향 그래프 간선의 분류

무향 그래프에서는 교차 간선이 없다. 또한 역방향, 순방향 간선도 없다. 

#### 🌱 위상 정렬의 정당성 증명

dfs(u)가 dfs(v)보다 일찍 종료할 경우, u에서 v로 가는 간선이 존재할 수 없다는 것을 증명하면 된다. 

#### 🌱 사이클 존재 여부 확인하기

사이클 존재 여부 = 역방향 간선 존재 여부

------

### 🌴간선을 구분하는 방법🌴

`discovered[]` : 각 정점을 몇 번째로 발견했는지 저장

dfs(u)에서 간선 (u,v)를 검사했을 때,

- v를 방문한 적이 없다. 👉 **`트리 간선`**

- v를 방문한 적이 있다. 
  - v가 u보다 늦게 발견되었다. (= v가 u의 자손) 👉 **`순방향 간선`**
  - v가 u보다 일찍 발견되었다. (= v는 u의 선조) 👉 **`역방향 간선`**
    - dfs(v) 종료 후, dfs(u) 종료 👉 **`교차 간선`**

#### ⌨️ 간선을 구분하는 깊이 우선 탐색의 구현

`discovered[i]` : i번 정점의 발견순서

`finished[i]` : dfs(i)가 종료했으면 1, 아니면 0

```c++
vector<vector<int>> adj;//인접리스트
vector<int> discovered, finished;
int counter;//전역변수
void dfs2(int here) {
  discovered[here] = counter++;//발견순서 
  for(int i=0; i<adj[here].size(); ++i) { //here의 인접노드만큼
    int there = adj[here][i]; //각 인접노드를 there로 설정하고
    if(discovered[there] == -1) {//there노드를 방문한 적 없다면
      cout<<'tree edge'<<endl; //트리 간선이다
      dfs2(there); //there 인접노드에 대해 dfs진행(재귀호출)
    }
    //there의 발견순서 값이 더 크면 here -> there순서이므로 순방향 간선이다
    else if(discovered[here] < discovered[there]) cout<<"forwared edge"<<endl;
    //here의 발견순서 값이 더 크고, dfs(there)이 종료하지 않았다면 역방향 간선이다
    else if(finished[there] == 0) cout<<"back edge"<<endl;
    //그 외의 경우는 모두 교차 간선이다
    else cout<<"cross edge"<<endl;
  }
  finished[here] = 1; //dfs종료 시,finished 값 재설정
}
```

-----

### 🌴 절단점(Cut Vertex) 🌴

#### 🌱 절단점(cut vertex)이란?

이 점과 인접한 간선들을 모두 지웠을 때, 해당 컴포넌트가 두 개 이상으로 나눠지는 정점

#### 🌱 절단점인지 확인하는 방법

해당 정점을 그래프에서 삭제 후 컴포넌트 개수가 늘어났는지 확인 👉 비효율적임

1. DFS 스패닝 트리를 만든다. 
2. 무향 그래프에는 교차간선 존재 x, 즉 어떤 정점 u와 연결된 정점들은 모두 u의 선조 혹은 자손이다.
3. 어떤 정점 u를 삭제했을 때, 컴포넌트 수가 늘어나지 않는 경우는 u의 선조/자손이 모두 역방향 간선으로 연결되어 있을 때 뿐이다.
4. 혹은 어떤 정점 u가 루트이고 u의 자손이 1이하인 경우에도 그래프가 쪼개지지 않는다. (그냥 홀라당 없어져버리기때문)

#### 🌱 이중 결합 컴포넌트(biconnected component)

무향 그래프에서 절단점을 포함하지 않는 서브그래프



### 📝 예제::절단점 찾기 알고리즘

한 번의 깊이우선탐색으로 모든 절단점을 출력하는 함수의 구현

#### ⌨️ 무향 그래프에서 절단점을 찾는 알고리즘💦

`findCutVertex()` : 매개변수 `here`를 루트로 하는 서브트리에 있는 절단점을 찾는 함수

```c++
vector<vector<int>> adj;
vector<int> discovered; //각 정점의 발견순서, -1로 초기화
vector<bool> isCutVertex; //각 정점의 절단점여부를 저장, false로 초기화
int counter = 0;//발견순서 저장하는 변수
int findCutVertex(int here, bool isRoot) {
  discovered[here] = counter++;//발견순서 값 갱신
  //ret : 해당 서브트리에서 역방향 간선으로 갈 수 있는 정점 중 가장 일찍 발견된 정점의 발견시점
  int ret = discovered[here];//ret에 현재 노드의 발견순서를 저장하고
  int children = 0;//자손 서브트리의 개수(루트인 경우, 자손이 2이상이어야 함)
  for(int i=0; i<adj[here].size(); ++i) {//인접노드에 대해
    int there = adj[here][i];//각 인접노드를 there이라 저장하고
    if(discovered[there] == -1) {//there 노드를 방문한 적이 없다면
      ++children;//일단 here의 자식노드 1개 추가해주고~
      //재귀호출로 자식노드 there이 루트인 서브트리에 절단점을 찾는다.
      int subtree = findCutVertex(there, false);
      //here가 루트가 아니면서 there서브트리의 절단점개수가 there의 발견 순서이상이면,
      //즉, 그 노드가 자기 자신 이하에 있다면 현재 위치는 절단점
      if(!isRoot && subtree >= discovered[there])
         isCutVertex[here] = true;
      ret = min(ret, subtree);
    }
    else 
      ret = min(ret, discovered[there]);
  }
  if(isRoot) //루트인 경우 자손이 2이상이면 절단점여부에 true
    isCutVertex[here] = (children >= 2);
  return ret;
}
```

----

### 🌴 다리(bridge) 🌴

어떤 간선을 삭제했을 때, 이 간선을 포함하던 컴포넌트가 두 개로 쪼개지는 경우, 그 간선을 **다리(bridge)**라고 한다.

- bridge는 항상 **Tree Edge**이다.
- (u, v) 간선을 제외하고, *u보다 높은 정점*💦에 갈 수 있는 역방향 간선이 존재하지 않는 경우, (u, v)는 bridge이다.
- 역방향 간선 중 자신의 부모로 가는 간선을 무시한 뒤, *v와 그 자손들에서 역방향 간선으로 닿을 수 있는 정점의 최소 발견 순서*가 u 이후라면 (u, v)는 bridge이다.💦

------

### 🌴 강결합 컴포넌트(Strongly Connected Components_SCC) 🌴

- 이중 결합 컴포넌트와 비슷하지만, 방향 그래프에서 정의되는 개념이다. 

- 방향 그래프에서 u와 v에 대해 양방향으로 가는 경로가 있을 때 두 정점은 같은 SCC에 속해있다고 한다. 

- 그래프에서 각 SCC 사이를 연결하는 간선들을 모으면 SCC들을 정점으로 하는 DAG(Directed Acylic Graph_사이클 없는 방향 그래프)를 만들 수 있다. 

- 그래프의 압축(Condensation) : 그래프의 정점들을 SCC별로 분리하고 각 SCC를 표현하는 정점들을 닺는 새로운 그래프를 만드는 과정

- 그래프가 두 개 이상의 SCC로 나눠지면, 한 지점에서 다른 지점으로 갈 수 없는 경우가 있다는 의미.

#### 🌱 타잔 알고리즘(Tarjain Algorithms)💦

- 한 번의 깊이 우선 탐색으로 각 정점을 SCC별로 분리한다.

1. DFS 스패닝 트리를 만든다. 
2. 이 때, 깊이 우선 탐색을 수행하면서 각 정점을 SCC로 묶는다. 

#### ⌨️ 타잔의 강결합 컴포넌트 분리 알고리즘의 구현💦

```

```

#### 🌱SCC의 위상정렬

새 SCC가 생겨나는 시점은 항상 scc()함수가 종료하기 직전이다. 

그래서 각 SCC는 위상정렬의 역순으로 번호가 매겨진다. (= 종료할 때 마다 저장된 SCC순서를 뒤집으면 위상정렬 결과이다.)

----

### 🌴 지배집합(dominating set)과 루트 없는 트리(unrooted tree) 🌴

#### 🌱 지배 집합(dominating set) 

그래프의 모든 정점을 지배하는 정점의 부분집합을 말하며, 이 때 각 정점이 자기 자신과 모든 인접한 정점들을 지배한다고 가정한다. 

**트리의 최소 지배 집합을 찾는 방법**

트리의 맨 아래에부터 시작해서 위로 올라오면서 각 노드의 선택 여부를 결정하는 알고리즘을 사용한다. 

- 잎 노드는 선택하지 않는다.(자신과 부모노드만 지배할 수 있기 때문)
- 이 외 노드는 다음의 조건 만족여부에 따라 노드를 선택할지, 선택하지 않을지 결정한다. 
  - 자손 중 아직 지배당하지 않은 노드가 있다면, 선택
  - 없다면, 선택하지 않는다.

#### 🌱 루트 없는 트리 (unrooted tree)

사이클이 존재하지 않는 그래프는 노드 간의 상하관계가 없을 뿐, 트리와 같은 형태를 가지는데 이를 루트 없는 트리라 한다. 

루트 없는 트리의 속성 (서로 동치관계)

- 정확히 V-1개의 간선이 있다. 
- 사이클이 존재하지 않는다.
- 두 정점 사이를 연결하는 단순 경로가 정확히 하나 있다. 

### 📝 예제::감시 카메라 설치(ID: GALLERY)

**🦘문제 🦘 **

 미술관에 감시 카메라 설치하려고 한다. 한 갤러리에 감시카메라를 설치하면 해당 갤러리 + 연결된 갤러리를 모두 감시할 수 있다고 할 때, 모든 갤러리를 감시하기 위해 필요한 최소 감시 카메라의 수를 구하는 문제.

⚡️**keypoint**⚡️

```c++
int V; //갤러리 수
vector<int> adj[MAX_V]; //인접행렬
vector<bool> visited; //방문여부 
const int UNWATCHED = 0;//감시되지 않은 갤러리
const int WATCHED = 1;//감시되는 갤러리
const int INSTALLED = 2;//설치된 카메라
int installed;//현재까지 설치된 카메라 수
int dfs(int here) {
    visited[here] = true;//방문여부 참으로 설정
    int childeren[3] = {0,0,0};//서브트리의 UNWATCHED, WATCHED, INSTALLED 정보저장
    for(int i=0; i<adj[here].size(); ++i) {//자손노드 수만큼
      int there = adj[here][i];//각 인접노드를 there로 설정하고
      if(!visited[there]) //아직 방문안했다면
         ++children[dfs(there)];//해당 노드의 children배열 정보 갱신
    }
    if(children[UNWATCHED]) {//아직 감시되지 않은 갤러리가 있다면
      ++installed;//카메라 설치해주고
      return INSTALLED;//설치되었다고 체크
    }
    if(children[INSTALLED])//설치된 카메라가 있다면 또 설치할 필요없고
      return WATCHED;//감시되는 갤러리 수 반환하고
    return UNWATCHED;//그 외에는 감시되지 않는 갤러리 수 반환
}
//그래프를 감시하는 데 필요한 카메라 최소 수 반환
int installCamera() {
    installed = 0;//현재까지 설치된 카메라 수
    visited = vector<bool>(V, false);//초기화
    for(int u=0; u<V; ++u) {//갤러리 수만큼
      //아직 방문하지 않았고 u가 아직 감시되지 않는 상태라면
      if(!visitied[u] && dfs(u) == UNWATCHED)
        ++installed;//카메라 설치
    }
    return installed;//총 개수 반환
}
```

⏱**Time Complexity**⏱

**O(g+h)**

-----

### 🌴 (2-)SAT문제 🌴 💦

참이냐, 거짓이냐의 결정을 여러 번 해야하는 문제들은 불린 값 만족성 문제(Boolean Satisfiability Problem) 혹은 SAT로 해결할 수 있다. 

#### 🌱 SAT 문제란? 

불린 값 변수의 참 형태와 거짓 형태들로 구성된 식이 주어질 때, 이 식의 값을 참으로 하는 변수의 조합이 있는지 찾는 것. 

#### 🌱 2-SAT 문제

논리식을 논리곱 정규형으로 표현했을 때 각 절에 최대 두 개의 변수만이 존재하는 SAT문제

그래프를 이용해 다항 시간에 해결할 수 있다. 

-----

## 🌞[종만북] 그래프의 너비 우선 탐색🌞

### 🌴너비 우선 탐색🌴

시작점에 가까운 정점부터 순서대로 방문하는 탐색 알고리즘

#### 🌱동작원리/과정

1. 각 정점을 방문할 때마다 모든 인접 정점들을 검사한다. 
2. 이 중 처음보는 정점을 발견하면 방문할 정점 목록 큐(queue)에 저장해놓는다. 
3. 인접한 정점들을 모두 검사하고나서, 방문할 정점 목록에서 다음 정점을 꺼내서 방문한다.

#### ⌨️ 그래프의 너비 우선 탐색

```c++
vector<vector<int>> adj;//인접리스트
vector<int> bfs(int start) {
  vector<bool> discovered(adj.size(), false);//발견여부 초기화
  queue<int> q;//방문할 정점 목록
  vector<int> order;//방문한 정점 목록
  discovered[start] = true;//시작노드의 발견여부: 참
  q.push(start);//방문할 정점 목록에 시작노드 추가
  while(!q.empty()) {//방문할 정점 목록이 있는 한
    int here = q.front();//방문할 정점 목록의 첫번쨰 
    q.pop();//방문했으니, 목록에서는 제거
    order.push_back(here);//방문한 목록에는 추가
    for(int i=0; i<adj[here].size(); ++i) {//인접목록에 대해
      int there = adj[here][i];//현재 인접목록을 there로 설정하고
      if(!discovered[there]) {//there을 아직 발견안했었다면
        q.push(there);//방문할 정점 목록에 추가하고
        discovered[there] = true;//발견여부는 참으로 설정
      }
    }
  }
  return order;//방문한 노드 순서목록을 반환
}
```

⏱**Time Complexity**⏱

인접 리스트로 구현한 경우  : **O(|V|+|E|)**

인접 행렬로 구현한 경우 : **O(|V|^2)**

#### 🌱 너비 우선 탐색 스패닝 트리(BFS Spanning Tree)

너비 우선 탐색에서 새 정점을 발견하는 데 사용했던 간선들만을 모은 트리

----

### 🌴너비 우선 탐색과 최단 거리🌴

**최단 경로 문제**: 두 정점을 연결하는 경로 중 가장 길이가 짧은 경로를 찾는 문제

- 시작점으로부터 다른 모든 정점까지의 최단 경로를 BFS Spanning Tree에서 찾을 수 있다. 

- BFS Spanning Tree에서 각 정점으로부터 트리의 루트인 시작점으로 가는 경로가 실제 그래프 상에서의 최단거리이다.