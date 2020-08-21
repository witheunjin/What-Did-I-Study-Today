# 2020.08.20_preview

[딕셔너리 공부]
https://wikidocs.net/16



## 타겟넘버

https://programmers.co.kr/learn/courses/30/lessons/43165

**문제** : 정수형 배열 numbers와 target number가 주어질 때, numbers를 더하거나 빼서 target number로 만들 수 있는 방법의 수 

**해결방법 : 재귀**

**입력데이터 한계** : 20 -> 데이터의 크기가 작으므로 어떤 알고리즘을 써도 괜찮다. 

**재귀로 풀 때 주의할 점** : 특수한 경우를 따로 처리해줘야 한다. + 종료조건 꼭 처리해줘야 한다. 



```python
#python
def solution(numbers, target) {
  if len(numbers)==0 and target==0:
    return 1
  elif len(numbers) == 0:
    return 0
  else:
    return solution(numbers[1:],target-numbers[0]) + solution(numbers[1:], target+numbers[0])
}
```



```
//c++

```



-------

## 완주하지 못한 선수

https://programmers.co.kr/learn/courses/30/lessons/42576

시도_실패

```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    
    string answer = "";
    for(int i=0; i<participant.size(); ++i) {
        vector<int>::iterator it = find(completion.begin(), completion.end(), participant[i]);        
        if(it != completion.end()) answer = *it;
        else completion.erase(it);
    }
    return answer;
}
```

find에서 잘못되었다고 함.

C++ onclinegdb에서 main함수랑 같이 실행해봄

```c++
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>
using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    
    string answer = "";
    for(int i=0; i<participant.size(); ++i) {
        vector<string>::iterator it;
        it = find(completion.begin(), completion.end(), participant[i]);        
        if(it != completion.end()) answer = *it;
        else completion.erase(it);
    }
    return answer;
}

int main()
{
    vector<string> p = {"aaa","bbb","ccc"};
    vector<string> c = {"aaa","bbb"};
    cout<<solution(p,c);
    return 0;
}

//실행결과 : bbb
```

이렇게 바꾸니까 됨

```c++
string solution(vector<string> participant, vector<string> completion) {
    
    string answer = "";
    for(int i=0; i<participant.size(); ++i) {
        vector<string>::iterator it;
        it = find(completion.begin(), completion.end(), participant[i]); 
        cout<<*it<<endl;
        if(it == completion.end()) answer = participant[i];
        else completion.erase(it);
    }
    return answer;
}
```

정확도는 통과, 근데 시간초과 ㅎ



-----------

## 비밀지도

https://programmers.co.kr/learn/courses/30/lessons/17681

..그래프

--------

## 프린터

https://programmers.co.kr/learn/courses/30/lessons/42587

우선순위큐

------

## 더맵게

https://programmers.co.kr/learn/courses/30/lessons/42626

..

------

## 전화번호 목록

https://programmers.co.kr/learn/courses/30/lessons/42577



------

## 수식최대화

https://programmers.co.kr/learn/courses/30/lessons/67257



-------

## 보석쇼핑

https://programmers.co.kr/learn/courses/30/lessons/67258



