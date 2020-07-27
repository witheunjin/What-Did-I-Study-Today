# 2020.07.27.Mon

**📚공부한 거 List**📚

- 종만북 - 26. 트라이
- 종만북 - (추가) 그래프로 풀 수 있는 문제 유형
- 종만북 - 28. 그래프의 깊이 우선 탐색

-----

## 🌴[종만북] 트라이🌴

#### 🌱 트라이(Trie)란?**

- 문자열의 집합을 표현하는 트리 자료구조로, 집합 내에서 원하는 원소를 찾는 작업을 **O(M)** (M은 문자열의 최대 길이) 만에 할 수 있게 한다. 

- 집합에 포함된 문자열의 접두사들에 대응되는 노드들이 서로 연결된 트리이다.

#### 🌱 트라이의 중요한 속성

- 트라이의 **root**는 항상 **길이 0인 문자열**에 대응되고, 노드의 깊이가 깊어질 때마다 문자열의 길이가 1씩 늘어난다. 
- **종료노드** : 해당 위치에 대응되는 문자열이 트라이가 표현하는 집합에 포함되어 있다는 의미
- 루트에서 한 노드까지 내려가는 경로에서 만나는 글자들을 모으면 해당 노드에 대응되는 문자열을 얻을 수 있다.
- **트라이의 노드 객체** = 자손 노드들을 가리키는 포인터 목록 + 종료노드인지 나타내는 boolean값 변수

#### ⌨️트라이의 노드를 표현하는 객체의 선언

`TrieNode` : 트라이의 노드 하나를 표현하는 객체 

`ALPHABET` : 문자열에 출현할 수 있는 문자의 개수

`toNumber()` : 주어진 문자를 숫자로 변환 (0~ALPHABET-1)

`insert()` : 트라이에 새 문자열을 추가하는 함수

`find()` : 트라이에 특정 문자열이 존재하는지 확인하는 함수

```
//필요한 헤더
#include <cstring> //memset
```

🚩주석 미완성부분있음

```c++
const int ALPHABETS = 26; //전체 알파벳 대문자 개수는 26개
int toNumber(char ch) {
  return ch - 'A';
}
struct TrieNode {
  TrieNode* children[ALPHABETS]; //자손노드들의 포인터 목록(동적배열이 아닌 고정배열 사용)
  bool terminal; //종료노드인가?
  TrieNode() : terminal(false) {//생성자(모든 트라이 노드의 종료노드여부를 false로 설정)
    memset(children, 0, sizeof(children));  //자손들의 포인터 목록을 0으로 초기화
  }
  ~TrieNode() { //소멸자
    for(int i=0; i<ALPHABETS; ++i) {
      if(children[i]) delete children[i]; 
    }
  }
  //이 노드를 루트로 하는 트리에 문자열 key를 추가
  void insert(const char* key) {
    if(*key == 0) terminal = true; //문자열이 끝나면 종료노드여부를 참으로 바꾼다
    else {
      int next = toNumber(*key);//문자열을 숫자로 변환 후 next에 저장
      if(children[next] == NULL) //next의 자식노드가 없다면
        children[next] = new TrieNode(); //자식노드 객체를 생성해준다
      children[next]->insert(key+1);//자식노드객체로 재귀호출
    }
  }
  //이 노드를 루트로 하는 트라이에 문자열 key와 대응되는 노드를 찾고 없으면 NULL반환
  TrieNode* find(const char* key) { 
    if(*key == 0) return this; //문자열이 끝났다면 this를 반환한다(?)
    int next = toNumber(*key); //문자열을 숫자로 변환 후 next에 저장
    if(children[next]==NULL) //자식노드가 없다면
      return NULL; //대응되는 노드가 없는 것이므로 NULL반환
    return children[next]->find(key+1);//자식노드 재귀호출
  }
}
```

-----



## 🌴 [종만북] 그래프로 풀 수 있는 문제유형 🌴

#### 🌱절단점 찾기 알고리즘 

- 철도망에서 한 역이 폐쇄된 경우, 철도망 전체가 두 개이상으로 쪼개질 가능성이 있는지 알아내는 문제
  - 역을 정점으로, 철로를 간선으로 표현하는 그래프를 만들고 절단점 찾기 알고리즘을 사용하여 해결

#### 🌱그래프의 너비 우선 탐색

- 친분관계를 표현하는 문제(몇 다리 건너야 아는 사이인지, 한 다리건너 아는 사람은 몇 명인지)
  - 사람을 정점으로, 관계를 간선으로 표현하는 그래프를 만들고 그래프의 너비 우선 탐색으로 해결

#### 🌱최소 스패닝 트리 알고리즘

- 두 컴퓨터 간 전송 용량 계산하는 문제(전송용량은 연결된 것들 중 최소 전송용량을 갖는 케이블에 좌우된다고 가정)
  - 컴퓨터와 라우터를 정점으로, 케이블을 간선으로 표현하는 그래프 생성 후, MST이용하여 해결

#### 🌱오일러 경로(자매품: 오일러 서킷)

- 한 붓 그리기 문제 
  - 깊이 우선 탐색을 응용한 오일러 경로를 통해 해결

#### 🌱최단 거리 알고리즘

- 가중치의 합이 음수인 사이클 찾기 문제 
- 최소한으로 타일을 움직여 15-퍼즐을 푸는 문제

#### 🌱위상정렬

- 어떤 순서대로 작업을 처리해야 하는지 계산하는 문제
  - 깊이 우선 탐색을 응용한 위상정렬 해결방법 이용

#### 🌱이분 매칭 알고리즘

- 일부 칸이 막혀있는 블록문제에서 막혀있지 않은 모든 칸에 블록을 놓는 문제
  - 상하좌우로 인접한 칸들을 간선으로 연결하는 그래프를 만들고 이분 매칭 알고리즘으로 해결

#### 🌱강 결합성 문제 (2-SAT)

- 만족성 문제 : 회의실 배정문제

#### 🌱깊이 우선 탐색

- 두 정점이 서로 연결되어 있는지 확인하는 문제
- 연결된 부분집합의 수 세는 문제
- 위상정렬
- 오일러 경로



-----



## 🌴 [종만북] 그래프의 깊이 우선 탐색 🌴

#### 🌱 오일러 트레일(Eulerian Trail)

그래프의 모든 간선을 정확히 한 번씩 지나지만, 시작점과 끝점이 다른 경로

오일러 트레일의 존재 조건 : 시작점과 끝점을 제외한 모든 점은 짝수점이고 시작점과 끝점은 홀수점이어야 한다. 

#### 🌱 해밀토니안 경로(Hamiltonian Path)

그래프의 모든 정점을 정확히 한 번씩 지나는 경로

모든 정점의 배열을 하나하나 시도하며 이들이 경로가 되는지 확인하는, 조합탐색으로 찾을 수 있다. (🤦‍♀️문제점 : 경우에 따라 너무 많은 후보가 있을 수 있음)

-----

### 📝 예제::단어 제한 끝말잇기(ID: WORDCHAIN)

단어들의 목록이 주어질 때, 단어들을 전부 사용하고 게임이 끝날 수 있는지, 그럴 수 있다면 어떤 순서로 단어를 사용해야 하는지를 계산하는 문제

⚡️**keypoint**⚡️

1. 입력에 주어진 각 단어를 간선으로 갖는 방향 그래프를 만들고, 정점은 간선의 첫 글자와 마지막 글자로 한다. 

#### ⌨️ 끝말잇기 문제의 입력을 그래프로 만들기

`adj` : 그래프의 인접행렬

`indegree`, `outdegree` : 각각 정점으로 들어오는 간선의 수, 나가는 간선의 수

`graph` : 두 정점 사이를 잇는 간선들이 나타내는 단어의 목록

```c++
vector<vector<int>> adj;
vector<string> graph[26][26];
vector<int> indegree, outdegree;

void makeGraph(const vector<string>& words) {
  for(int i=0; i<26; ++i) {
    for(int j=0; j<26; ++j) 
      graph[i][j].clear();
  }
  adj = vector<vector<int>>(26, vector<int>(26,0));
  indegree = outdegree = vector<int>(26,0);
  for(int i=0; i<words.size(); ++i) {
    int a = words[i][0] - 'a';
    int b = words[i][words[i].size()-1] - 'a';
    graph[a][b].push_back(words[i]);
    adj[a][b]++;
    outdegree[a]++;
    indegree[b]++;
  }
}

```

### 🌱 방향 그래프에서의 오일러 서킷/트레일

**방향 그래프에서 오일러 서킷의 존재 조건**

- 각 정점에 들어오는 간선의 수와 나가는 간선의 수가 같아야 한다.

**방향 그래프에서 오일러 트레일의 존재 조건**

- 시작점이 a, 끝점이 b일 때, `a에서 나가는 간선의 수 = 들어오는 간선의 수 + 1` 이 되어야하고, b에서는 `들어오는 간선의 수 = 나가는 간선의 수 + 1`이어야 한다. 

#### 🌱 오일러 서킷 vs 오일러 트레일

각 정점의 차수를 확인하자!

#### ⌨️ 방향 그래프에서 오일러 서킷 혹은 오일러 트레일 찾아내기

`getEulerCircuit` : 오일러 서킷 혹은 트레일의 경로를 계산

``` c++
void getEulerCircuit(int here, vector<int>& circuit) {
  for(int there=0; there<adj.size(); ++there) { //모든 정점에 대해
    while(adj[here][there] > 0) {//연결된 정점이 있는 한
      adj[here][there]--; //<here-there> 간선은 감하고
      getEulerCircuit(there, circuit); //연결된 정점에 대해 함수재귀호출
    } 
  }
  circuit.push_back(here); //경로에 추가
}
```

`getEulerTrailOrCircuit` : 현재 그래프의 오일러 트레일이나 서킷을 반환

```c++
vector<int> getEulerTrailOrCircuit() {
  vector<int> circuit;
  for(int i=0; i<26; ++i) { //모든 문자정점에 대해 
    if(outdegree[i] == indegree[i] + 1) {//나가는 간선이 들어오는 간선보다 한 개 더 많은 경우라면, 오일러 트레일
      getEulerCircuit(i, circuut); //경로를 계산한다
      return circuit; //계산된 경로를 반환
    }
  }
  for(int i=0; i<26; ++i) { //모든 문자 정점에 대해
    if(outdegree[i]) { //오일러 트레일이 아니면 오일러 서킷
      getEulerCircuit(i, circuit); //경로를 계산한다
      return circuit; //계산된 경로를 반환
    }
  }
  return circuit; //경로 계산에 실패했으면 빈 배열 반환
}
```

#### 🌱 오일러 서킷/트레일의 존재 여부 확인

존재 조건 확인하기!

#### ⌨️ 끝말잇기 문제를 오일러 트레일 문제로 바꿔 해결하는 알고리즘

(= 오일러 트레일이 존재하는지 확인하고, 존재하는 경우 출력 문자열을 계산해 반환하는 알고리즘)

`checkEuler()` : 현재 그래프의 오일러 서킷/트레일 존재 여부를 확인하는 함수

`solve()` : 경로를 문자열로 반환하여 출력하는 함수

📢 **<참고> 일부 변수명을  바꾸었으나, 코드내용은 책과 동일합니다. **

```c++
bool checkEuler() {
  int startCnt = 0; //예비시작점개수 카운트
  int endPoint = 0; //예비끝점개수 카운트
  for(int i=0; i<26; ++i) {
    int diff = outdegree[i] - indegree[i];//입출간선 개수차이
    if(diff < -1 ||diff > 1) return false; //차이가 +1초과, -1미만이면 오일러 서킷/트레일 안됨
    if(diff == 1) startCnt++; //나가는 간선이 더 많으면 예비시작점 개수 +1
    if(diff == -1) endCnt++; //들어오는 간선이 더 많으면 예비끝점 개수 +1
  }
  //총 계산된 예비시작점, 예비끝점 개수가 1일 때(=오일러 트레일) 혹은
  //둘 다 0일 때(=오일러 서킷)만 true반환
  return (startCnt==1 && endCnt==1) || (startCnt==0 && endCnt==0)
}
```

```c++
string solve(const vector<string>& words) {
  makeGraph(words); //그래프 만들고
  if(!checkEuler()) return "IMPOSSIBLE"; //오일러 서킷/트레일 아니면 impossible반환
  //아니라면 오일러 서킷이나 트레일이라는 것이므로
  vector<int> circuit = getEulerTrailOrCircuit(); //계산된 경로를 circuit에 저장
  if(circuit.size() != words.size()+1) return "IMPOSSIBLE"; //모든 간선을 방문했는지 확인
  //여기까지왔다면, 정상적인 오일러 서킷/트레일 경로라는 것이므로
  reverse(circuit.begin(), circuit.end()); //경로 순서를 바꿔주어 시작점부터 끝점 순서로 배열해주고
  string ret; //답으로 출력하게 될 문자열 변수 생성
  for(int i=0; i<circuit.size(); i++) {//경로의 정점 수만큼
    int a = circuit[i-1]; //시작점
    int b = circuit[i]; //끝점
    if(ret.size()) ret += " "; //정점 사이에 공백문자열 추가해주고
    ret += graph[a][b].pop_back(); //문자열에 정점 저장
  }
  return ret; //결과 반환
}
```

⏱**Time Complexity**⏱

**O(nA)** : n은 단어의 수, A는 알파벳의 수

-----

