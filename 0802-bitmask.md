# 2020.08.02 Sun

### **📚공부한 거 List**📚

- bitmask

------

## Bitmask로 문자열에 같은 문자 없는지 확인하기

```c++
bool isUnique(const string str) {
  bitset<256> bits(0);
  for(int i=0; i<str.length(); ++i) {
    int val = str[i];
    if(bits.test(val) > 0) return false;
    bits.set(val);
  }
  return true;
}
```

----

### bitset 선언하기

bitset<크기> 이름(초기화할 값)

```c++
int main() {
    bitset<3> bits(0);
    for(int i=0; i<3; ++i) {
        cout<<bits[i]<<' ';
    }
    return 0;
}
```

결과 : 0 0 0

```c++
int main() {
    bitset<3> bits(1);
    for(int i=0; i<3; ++i) {
        cout<<bits[i]<<' ';
    }
    return 0;
}
```

결과 : 1 0 0 

```c++
bitset<3> bits(2);
```

결과 : 0 1 0

```c++
bitset<3> bits(3);
```

결과 : 1 1 0

```c++
bitset<3> bits(4);
```

결과 : 0 0 1

------

### bits.test(n)

인덱스 n번째 비트가 켜져있는지 여부 반환

```c++
int main() {
    bitset<3> bits(3);
    for(int i=0; i<3; ++i) {
        cout<<boolalpha<<bits.test(i)<<' ';
    }
    return 0;
}
```

결과 : true true false 

-----

### bits.set(n)

n번째 인덱스 비트값을 1로 설정

```c++
int main() {
    bitset<3> bits(3);
    bits.set(2);
    for(int i=0; i<3; ++i) {
        cout<<boolalpha<<bits.test(i)<<' ';
    }
    return 0;
}
```

결과 :  true true true