# 2020.08.20_preview

[딕셔너리 공부]
https://wikidocs.net/16



## 타겟넘버

https://programmers.co.kr/learn/courses/30/lessons/43165

?.?

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



