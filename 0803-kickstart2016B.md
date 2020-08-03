# 2020.08.03 Mon

#### 📚공부한 거 List📚

- Kickstart 2016 Round B 기출문제 풀기
  - Sherlock and Parentheses
  - Sherlock and Watson Gym Secrets
  - Watson and Intervals

------

### 회고 

#### 문제 푸는 시간

40분 (Start_16:46 ~ End_17:26)

#### 문제 푸는 동안 한 거

3문제 읽고 바로 풀기 (마지막 문제는 읽지도 못함)

#### 아쉬웠던 점

동아리 프로젝트로 인해 복습까지 못했다.

아직 모르는 단어가 많아서 문제이해가 쉽지 않았다. 거의 샘플케이스보고 유추했던 것 같다. 

--------

## Sherlock and Parentheses

소요 시간

- 1차 : 22 mins

#### ☑️ check-check ☑️

- [x] 문제를 이해하였나

- [x] 풀이 방법이 빨리 생각났나

- [ ] Small dataset을 통과하였나

- [ ] Large dataset을 통과하였나

  cf. 문제는 풀었는데 실행은 못해봄

#### 🙄 잘한 점, 아쉬웠던 점 🙄

- **잘한 점 **
  - 빨리 풀었다. 

- **아쉬웠던 점 **
  - 시간복잡도 생각않고 풀었다.
  - parentheses가 뭔지 몰랐다. 
  - 문제가 아니라 샘플 입출력 데이터를 보고 문제를 이해했다. 

#### 🧐 다른 풀이방법에는 뭐가 있을까 🧐

-

#### ⌨️ 손 코드 ⌨️

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int isBalanced(int left, int right) {
  if(left==0 && right==0) return 1;
  if(left==0 || right==0) return 0;
  if(left == right) return left;
  int smaller = min(left, right);
  return smaller*(smaller-1)/2;
}
int main() {
  int T=0, L=0, R=0;
  cin >> T; 
  for(auto t:T) {
    cin>>L>>R;
    cout<<"Case #"<<t+1<<":"<<isBalanced(L,R)<<endl;
  }
  return 0;
}
```

------------

## Sherlock and Watson Gym Secrets

소요 시간 

- 1차 : 16 mins  

#### ☑️ check-check ☑️

- [x] 문제를 이해하였나
- [x] 풀이 방법이 빨리 생각났나
- [ ] Small dataset을 통과하였나
- [ ] Large dataset을 통과하였나

#### 🙄 잘한 점, 아쉬웠던 점 🙄

- **잘한 점 **
  - 문제 이해가 빨랐고, 풀이 방법이 나름 빨리 생각났다.

- **아쉬웠던 점 **
  - 시간복잡도 생각않고 풀었다. 3중 for문이 웬 말,,,
  - is divisible by 의 뜻을 몰랐다. 나누어지냐는 뜻.(= 나머지가 0이냐)
  - large dataset, small dataset 모두 테스트 못해봤다.

#### 🧐 다른 풀이방법에는 뭐가 있을까 🧐

-

#### ⌨️ 손 코드 ⌨️

```c++
#include <iostream>
#include <cmath>
using namespace std;
int a=0, b=0, n=0, k=0;
bool isValid(int i, int j) {
  if(i>n || j>n) return false;
  int x = pow(i,a);
  int y = pow(j,b);
  if((x+y)%k == 0) return true;
  return false;
}
int main() {
  int T=0;
  for(auto t : T) {
    cin>>a>>b>>n>>k;
    int result=0;
    for(int i=0; i<n; i++) {
      for(int j=0; j<n; j++) {
        if(isValid(i,j)) ++result;
      }
    }
    cout<<"Case #"<<t+1<<":"<<result<<endl;
  }
  return 0;
}
```

---------

## Watson and Intervals

소요 시간

- 1차 : 17 mins

#### ☑️ check-check ☑️

- [ ] 문제를 이해하였나
- [ ] 풀이 방법이 빨리 생각났나
- [ ] Small dataset을 통과하였나
- [ ] Large dataset을 통과하였나

#### 🙄 잘한 점, 아쉬웠던 점 🙄

- **잘한 점 **
  - 

- **아쉬웠던 점 **
  - 문제 이해가 아예 안됐다.
  - 모르는 단어가 많았다. (intricacies, recurrences, intervalm inclusive, modulo ...)
  - 단어를 몰라도 문맥상 유추하는 연습이 필요한 것 같다. 

#### 🧐 다른 풀이방법에는 뭐가 있을까 🧐

-

