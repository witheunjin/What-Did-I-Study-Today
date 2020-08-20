# 2020.08.20_review

SW코딩 입사테스트 합격대비반 수업내용정리

공부가 더 필요하다고 느낀 부분 : DP, <cmath>, 소수점자리 출력(cout)

----

## 문자열뒤집기

입력된 문자열을 거꾸로 뒤집어 출력

#### C++_reverse 이용

```c++
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
  string str;
  cin >> str;
  reverse(str.begin(), str.end());
  cout << str;
  return 0;
}
```
#### Py_반복문 이용

```python
# for문을 이용한 방법
s = input() //입력받은 것을 s에 넣어줌
s_reversed = '' //결과
for c in s: //문자열의 각 문자원소를
    s_reversed = c + s_reversed //결과 문자열에 추가해줌
print(s_reversed) //출력

#좀 더 간단한 방법
s = input()		
print(s[::-1]) //s의 전체 범위에 대해 1씩 감소한 것을 출력

```

----

### 소수 판별

#### C++_에라토스테네스의 체 이용

```c++
#include <iostream>
using namespace std;

bool aratos(int n) {
  if(n<2) return false;
  for(int i=2; i<n; ++i) {
    if(n%2 == 0) return false;
  }
  return true;
}

int main() {
  int n;
  cin>>n;
  if(aratos(n)) cout<<"True";
  else cout<<"False";
  return 0;
}
```

#### py_에라토스테네스의 체 이용

```python
n = int(input())
is_prime = True

if n == 1:
	is_prime = False
else:
	for x in range(2, n):
		if n % x == 0:
			is_prime = False

print(is_prime)
```

#### 💦 py_절댓값이용한 범위제한

```python
#solution 1
import math

n = int(input())
is_prime = True

if n == 1:
	is_prime = False
else:
	for x in range(2, int(math.sqrt(n)) + 1):
		if n % x == 0:
			is_prime = False

print(is_prime)

#solution 2
import math

n = int(input())
is_prime = True

if n == 1:
	is_prime = False
else:
	if n % 2 == 0 and n != 2:
		is_prime = False
	else:
		for x in range(3, int(math.sqrt(n)) + 1, 2):
			if n % x == 0:
				is_prime = False

print(is_prime)
```

---------

### 괄호 짝 맞추기

#### C++_스택

```c++
#include <iostream>
#include <stack>
using namespace std;

bool isMatched(const string& str) {
  const string open("[{("), close("]})"); //순서 조심해라
  stack<char> s;
  for(int i=0; i<str.length(); ++i) {
    if(open.find(str[i]) != -1) //str[i]가 open에 있으면
      s.push(str[i]);
    else {
      if(open.empty()) return false;
      //s.top의 open에서의 인덱스와 str[i]의 close에서의 인덱스 불일치 시
      //괄호의 짝이 맞지 않으므로 false반환
      if(open.find(s.top()) != close.find(str[i])) return false;
      s.pop();
    }
  }
  return s.empty(); //결과적으로 스택이 비어있어야 최종적으로 괄호짝이 다 맞은거.
}

int main() {
  string str;
  cin >> str;
  if(isMatched(str)) cout<<"True";
  else cout<<"False";
  return 0;
}
```

#### py_스택

```python
s = input()

a = b = c = 0

answer = True
stack = []

#3가지의 닫는 괄호 각각에 대해서 매칭되는 여는 괄호를 정의한다.
d = { ')':'(', '}':'{', ']':'[' }

for x in s:

#여는 괄호라면 스택에 넣는다.
	if x == '(' or x == '{' or x == '[':
		stack.append(x)
	else:
#닫는 괄호가 나오면 스택에서 여는 괄호를 꺼내서 지금의
#닫는 괄호와 매칭이 되는지 비교한다. 
#매칭 되지 않거나, 스택이 비어 있다면 잘못된 괄호 문자열이다.
		if len(stack) == 0 or stack.pop() != d[x]:			
			answer = False
			break
		
		
#for문이 종료된 후에도
#스택에서 아직 여는 괄호가 남아있다면 잘못된 괄호 문자열이다.
if len(stack) != 0 :
	answer = False

print(answer)

```

-------

### 타일채우기

아직 안 풀었음 주말까지 풀기 

dp로도 풀 수 있고 뭐 다른 방법도 있었던 것 같은데 최대한 다양한 방법으로 풀어보기

----

### 다이아몬드 최대합 구하기

#### 💦 C++_DP 

```

```

#### py_DP

```python
n = int(input())

a = []

for i in range(n):
	t = input()
	# 공백으로 문자열을 분리한 후, 리스트에 집어 넣는다.
	a.append([int(x) for x in t.split()])
	
	for j in range(len(a[i])):
		if i > 0: #첫 행이 아닌 경우에만 실행함
			if j == 0: #첫 열이라면 선택의 여지가 없음
				a[i][j] = a[i-1][j] + a[i][j]
		  
			if j == len(a[i])-1:#마지막 열이라면 선택의 여지가 없음
				a[i][j] = a[i-1][j-1] + a[i][j]
			
			if j > 0 and j < len(a[i]) - 1:#두 값중에서 큰 값을 선택함			
				a[i][j] = max(a[i-1][j-1] , a[i-1][j]) + a[i][j]
							
		
for i in range(n - 1):
	t = input()
	a.append([int(x) for x in t.split()])
	for j in range(len(a[-1])):
		#숫자의 개수가 줄어드는 아랫 부분 행에서는 두 값중에서 큰 값을 선택함
		a[-1][j] = max(a[-2][j] , a[-2][j+1]) + a[-1][j]
		
#마지막 행의 마지막 값을 출력함		
print(a[-1][-1])

```

