# 2020.08.08 Sat (1)

## Kickstart 2016 Round A_Country Leader

### Problem

The Constitution of a certain country states that the leader is the person with <u>the name containing the greatest number of different alphabet letters.</u> (The country uses the <u>uppercase</u> English alphabet from A through Z.) For example, the name `GOOGLE` has four different alphabet letters: E, G, L, and O. The name `APAC CODE JAM` has eight different letters. If the country only consists of these 2 persons, `APAC CODE JAM` would be the leader.

<u>If there is a tie, the person whose name comes earliest in alphabetical order is the leader.</u>

Given a list of names of the citizens of the country, can you determine who the leader is?

### Input

The first line of the input gives the number of test cases, **T**. **T** test cases follow. Each test case starts with a line with an interger **N**, the number of people in the country. Then **N** lines follow. The <u>i-th line</u> represents the <u>name of the i-th person</u>. Each name contains at most 20 characters and contains at least one alphabet letter.

### Output

For each test case, output one line containing `Case #x: y`, where `x` is the test case number (starting from 1) and y is the name of the leader.

### Limits

1 ≤ **T** ≤ 100.
Time limit: 20 seconds per test set.
Memory limit: 1GB.
1 ≤ **N** ≤ 100.

#### Small dataset (Test set 1 - Visible)

Each name consists of at most 20 characters and only consists of the uppercase English letters `A` through `Z`.

#### Large dataset (Test set 2 - Hidden)

Each name consists of at most 20 characters and only consists of the uppercase English letters `A` through `Z` and ' '(space).
All names start and end with alphabet letters.

### Sample

| Input                                                        | Output                                |
| ------------------------------------------------------------ | ------------------------------------- |
| 2<br/>3 <br/>ADAM <br/>BOB <br/>JOHNSON <br/>2 <br/>A AB C <br/>DEF | Case #1: JOHNSON <br/>Case #2: A AB C |

In sample case #1, `JOHNSON` contains 5 different alphabet letters('H', 'J', 'N', 'O', 'S'), so he is the leader.

Sample case #2 would only appear in Large data set. The name `DEF` contains 3 different alphabet letters, the name `A AB C` also contains 3 different alphabet letters. `A AB C` comes alphabetically earlier so he is the leader.

----------

### Solution

using...

1. Brute-Force(Small/Large Dataset)
2. Bitmask
3. Priority_Queue

--------

### Solution using Brute-Force_Small Dataset

`diffAlphabet(const string& name)`  : return the number of alphabet in the name

```c++
#include <iostream>
#include <vector>
using namespace std;

vector<bool> alphabet;

int diffAlphabet(const string& name) {
    alphabet = vector<bool>(26,false); //initialize the array(A-Z)
    int cnt; //the number of alphabet in the name
    for(int a=0; a<name.length(); ++a) {
        int val = name[a]; //val is the location of the character in vector
        if(!alphabet[val]) {//when the character hasn't been discovered,
            alphabet[val] = true; //set the element in the array to 'true'
            cnt++;//increase the value of 'cnt'
        }
    }
    return cnt;//return it
}

int main() {
    int T=0; //T is the number of Test Case
    int N=0; //N is the number of people
    cin >> T;
    for(int t=0; t<T; ++t) { //for each test case
        cin >> N;
        int prev = 0; //object to compare
        string leader; //name of leader so far
        for(int i=0; i<N; ++i) { 
            string name; //name of current person
            cin>>name;
            if(!i) {//if there isn't an object to compare,
                prev = diffAlphabet(name); //set the current name to 'prev'
                leader = name; //set the current person to leader
            }
            else {
                int cur = diffAlphabet(name);//set current name to 'cur'
                //when 'prev' contains more alphabet or
                //if 'prev' and 'cur' is a tie, 'prev' is earlier in alphabetical order,
                if((prev < cur)||(prev == cur && leader[0]>name[0])) {
                    prev = cur; // set 'cur' to 'prev'
                    leader = name;//and set i-th person to 'leader'
                }
            }
        }
        cout<<"Case #"<<t+1<<":"<<leader<<endl;
    }
    return 0;
}
```

------

### Solution using Brute-Force_Large Dataset

`Solution using Brute-Force_Small Dataset`에서 `#include <string>`을 추가하고, 

name 입력받는 부분을 

```c++
getline(cin, name);
```

으로 수정하면 된다. 여기서 주의할 점은 `cin`으로 입력받고 `getline`으로 입력받을 때는 `getline`이전에 

```
cin.ignore();
```

을 꼭! 써줘서 버퍼를 비워줘야한다. 