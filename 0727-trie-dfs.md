# 2020.07.27

**📚공부한 거 List**📚

- 종만북 - 26. 트라이
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



## 🌴 [종만북] 그래프의 깊이 우선 탐색 🌴