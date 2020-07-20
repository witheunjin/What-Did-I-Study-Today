# 2020.07.20 Mon

##### **📚공부한 거 List📚**

- 종만북 - 비트마스크

-----

## 비트마스크

정의 : 정수의 이진수 표현을 자료구조로 쓰는 기법

#### 원소 20개의 공집합/꽉 찬 집합 만들기 

```
int emptySet = (1<<20);
int fullSet = (1<<20)-1;
```

#### n번째 원소 추가하기/유무확인하기

```
elements |= (1<<n);
if(elements & (1<<n))
```

#### n번째 원소 삭제하기(1) - 원래 있는 경우에만

```
elements -= (1<<n);
```

#### n번째 원소 삭제하기(2) - 원소의 유무 상관없이

```
elements &= ~(1<<n);
```

#### 토글하기(있으면 없도록, 없다면 있도록 만들기)

```
elements ^= (1<<n);
```

#### 집합의 크기 구하기

```c++
int bitCount(int x) {
  if(x==0) return 0;
  return x%2 + bitCount(x/2);
}
```

#### 집합에서 가장 작은 원소 찾기 (어디 있는지) -> 켜져 있는 최하위 번호를 반환하면 됨

```c++
int minElement = (elements & -elements);
```

#### 최소 원소 지우기(2의 거듭제곱인지 확인할 때 유용하게 쓰임)

```c++
elements &= (elements-1);
```

*2의 거듭제곱은 켜진 비트가 1개 밖에 없다. 즉, 최하위 비트 삭제 시 전체 값이 0이 되는지 확인하면 된다. 

#### 모든 부분 집합 순회하기

```c++
for(int subset = set; subset; subset = ((subset-1) & set))
```

`subset-1` : 최하위 비트는 끄고, 그 아래 비트는 모두 켜진 상태로 만든다.





## 에라토스테네스의 체

#### k가 소수인지 확인하는 함수

```c++
inline bool isPrime(int k) {
  return sieve[k>>3] & (1<<(k&7));
}
```

#### k가 소수가 아니라고 표시하는 함수 (= 소수집합에서 k를 삭제하는 함수)

```c++
inline void setComposite(int k) {
  sieve[k>>3] &= ~(1<<(k&7));
}
```



## 15퍼즐

64bit = 4bit * 16

퍼즐의 상태를 64비트로 표현할 수 있다.

#### 64비트 정수 변수 선언

```c++
typedef unsigned long long uint64;
```

#### 해당 인덱스에 있는 값을 구하는 함수

```c++
/* 
 * @param mask [number storing the state of the puzzle]
 * @param index [position to be changed the value]
 */
int get(uint64 mask, int index) {
  return (mask >> (index <<2)) & 15;
}
```

#### 해당 인덱스에 값을 설정하는 함수

```c++
/* 
 * @param mask [number storing the state of the puzzle]
 * @param index [position to be changed the value]
 * @param value [new value of the index]
 */
uint64 set(uint64 mask, int index, uint64 value) {
  return mask & ~(15LL << (index<<2)) | (value << (index<<2));
}
```



## 극대 안정 집합

같이 두면 폭발하는 물질들이 상존하지 않는 집합을 구하는 문제

#### 집합에 물질 i와 같이 두면 안되는 물질이 있는지 확인하는 핵심코드

```c++
/*
 * set : 물질들의 집합
 * i : 물질의 인덱스 값
 * explodes[i] : i와 같이 두면 폭발하는 물질들의 집합
 */
(set & (1<<i)) && (set & explodes[i])
```

