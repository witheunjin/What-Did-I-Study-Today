# 2020.07.21 Tue

**📚공부한 거 List**📚

- 코딩인터뷰완전분석 - 트리와 그래프 이론 정리
- 종만북 - 21. 트리의 구현과 순회 ('요새' 제외)
- 종만북 - 22. 이진검색트리 ('트립', '삽입 정렬 뒤집기' 제외)
- 종만북 - 27. 그래프의 표현과 정의
- 종만북 - 28. 그래프의 깊이 우선 탐색

----

## [종만북] 트리의 구현과 순회

#### ⌨️트리의 노드를 표현하는 객체

```c++
struct TreeNode {
  string label; //value
  TreeNode* parent;
  vector<TreeNode*> children;
};
```

### 트리의 순회(traversal)

- 모든 노드를 순회하며 데이터 출력
- 트리의 높이구하기(height(tree) = max(depths(subtree)))
- 순회 종류 : `pre-order`(VLR), `in-order`(LVR), `post-order`(LRV)

#### ⌨️트리를 순회하며 모든 노드에 포함된 값 출력

```c++
void printLables(TreeNode* root) {
  cout << root->label << endl;
  for(int i=0; i<root->children.size(); ++i) {
    printLables(root->children);
  }
}
```

#### ⌨️트리를 순회하여 트리의 높이 계산

```c++
int height(TreeNode* root) {
  int h=0;
  for(int i=0; i<root->children.size(); ++i) {//루트의 자식 수만큼
    //root->children[i] : 루트의 i번째 자식
    h = max(h, 1 + height(root->children[i]));
  }
  return h;
}
```

### 📝예제::트리 순회 순서 변경(ID: TRAVERSAL)

**문제** : 전위순회했을 때 노드방문순서(preorder)와 중위순회했을 때 노드방문순서(inorder)가 입력으로 주어졌을 때, 이 트리를 후위순회했을 때 노드들의 방문순서를 출력.

⚡️**keypoint**⚡️

1. 전위순회 시, 처음으로 방문하는 노드가 그 트리의 루트노드이다. 
2. 중위순회 시, 루트노드를 기준으로 이전에 방문한 노드들은 루트보다 작은 값을 가지며, 이후에 방문한 노드들은 루트보다 큰 값을 가진다. 
3. 그러므로 preorder[0]이 rootnode임을 저장하고, inorder에서 rootnode의 위치를 찾은 후, 재귀호출을 이용해 후위순회를 하면된다. 

🔑**해답(코드)**🔑

```c++
/*
 * 배열 v를 구간 [a,b]로 쪼개는 함수
 * @param v [쪼개려는 배열(트리)]
 * @param a [시작구간]
 * @param b [끝구간]
 */
vector<int> slice(const vector<int>& v, int a, int b) {
  return vector<int>(v.begin()+a, v.begin()+b);
}
```

```c++
void printPostOrder(const vector<int>& preorder, const vector<int>& inorder) {
  const int N = preorder.size();
  if(preorder.empty()) return;
  const int root = preorder[0];
  const int L = find(inorder.begin(), inorder.end(), root) - inorder.begin();
  const int R = N - 1 - L;
  printPostOrder(slice(preorder, 1, L+1), slice(inorder, 0, L));
  printPostOrder(slice(preorder, L+1, N), slice(inorder, L+1, N));
  cout<<root<<' ';
}
```

_____________

## [종만북] 이진 검색 트리(BST)

- 검색 트리는 자료들을 **일정한 순서**에 따라 정렬된 상태로 저장한다. 그렇기 때문에 원소의 추가/삭제 연산과 특정원소를 찾는 연산이 매우 빠르게 동작한다. 
- 이진트리의 정의 : 최대 두 개의 자식노드를 갖는 트리 
- 이진 검색 트리를 중위 순회하면 크기 순서로 정렬된 원소의 목록을 얻는다. 즉, 최대원소와 최소원소를 쉽게 얻을 수 있다. **중위순회 시 가장 첫번째로 방문하는 노드는 최소값을, 가장 마지막에 방문하는 노드는 최대값을 갖는다. **
- **트립(Treap)** : 주어진 값 X보다 작은 원소의 수, 혹은 (크기순으로 정렬되었다고 가정) k-번째 원소를 찾는 연산들을 수행하는데 사용한다. 
- 균형 잡힌 이진 검색 트리(balanced BST) : 트리의 높이가 항상 **O(lgN)**이 되도록 하는 트리. (ex. 레드-블랙 트리_Red-Black Tree)

### 📝예제::너드인가, 너드가 아닌가? 2 (ID: NERD2)

**문제** : 너드지수를 계산하는 기준은 1. 푼 문제의 수/ 2. 새벽에 먹은 라면그릇수 이다. 만약 타 참가자보다 푼 문제의 수가 적고, 새벽에 먹은 라면 그릇 수가 적다면 이 사람은 대회자격이 없다고 판단한다. 이 때, 각 사람이 참가신청을 할 때마다 대회에 참가할 수 있는 사람들의 수가 어떻게 변하는지 계산하는 프로그램 작성.

⚡️**keypoint**⚡️

1. map<int, int>를 이용해 균형잡힌 BST를 구현한다. 
2. lower_bound(x) 는 x이상의 값 중 가장 작은 값을 반환하는 STL이다. 
3. 만약 새 참가자의 x좌표(문제 수)값의 lower_bound를 가지는 참가자 K가 새 참가자를 지배한다면, 그보다 큰 x좌표를 갖는 참가자와는 비교할 필요가 없다. 왜냐하면 좌표의 우측으로 갈수록 y좌표값은 작아지고, x좌표값은 커지기 때문이다. 

🔑**해답(코드)**🔑

```c++
map<int,int> coords; //각 참가자들의 데이터(x,y)

bool isDominated(int x, int y) {
  map<int,int>::iterator it = coords.lower_bound(x);
  if(it == coors.end()) return false;
  return y < it->second;
}
```

```c++
void removeDominated(int x, int y) {
  map<int,int>::iterator it = coords.lower_bound(x);
  if(it == coords.begin()) return;
  --it;
  while(true) {
    if(it->second > y) break;
    if(it == coords.begin()) {
      coords.erase(it);
      break;
    }
    else {
      map<int,int>::iterator jt = it;
      --jt;
      coords.erase(it);
      it = jt;
    }
  }
}
```

```c++
int registered(int x, int y) {
  if(isDominated(x,y)) return coords.size();
  removeDominated(x,y);
  coords[x] = y;
  return coords.size();
}
```

**⏱Time-Complexity⏱**

**O(N lgN)**

