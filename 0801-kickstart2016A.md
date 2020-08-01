# 2020.08.01 Sat

### 📚공부한 거 List📚

- Kickstart 2016 round A 기출문제 풀기
  - [Country Leader](#country-leader) 👉[문제](country-leader_problem)
  - [Rain](#rain) 👉[문제](rain_problem)
  - [Jane's Flower Shop](#jane's-flower-shop) 👉[문제](jane's-flower-shop_problem)
  - [Clash Royale](#clash-royale) 👉[문제](clash-royale_problem)

-----

## 회고

#### 문제 푸는 시간 

 1시간 20분(80분) / limit : 3시간(180분)

#### 문제 푸는 동안 한 거

 4문제 문제 이해 + sample dataset 이해 + 첫번째 문제 풀기

#### 아쉬웠던 점

동아리 프로젝트 때문에 3시간동안 계속 진행하지 못한 점..ㅠ

영어로 문제 이해하는 게 아직 익숙하지 않다. 

------

## Country Leader

#### ☑️ check-check ☑️

- [x] 문제를 이해하였나
- [x] 풀이 방법이 빨리 생각났나
- [x] Small dataset을 통과하였나
- [ ] Large dataset을 통과하였나

#### 🙄 잘한 점, 아쉬웠던 점 🙄

- **잘한 점 **
  - 빨리 풀었다. 

- **아쉬웠던 점 **
  - 시간복잡도 생각않고 빨리 푸는 데 급급했던 것 같다. 
  - bitmask랑 우선순위 큐, map으로 풀 수 있을 것 같다는 생각만 들고 구현을 못했다.
  - Large Dataset에서 공백을 포함한 문자열 입력받는 방법이 생각안나서 못 풀었다. 

#### 🧐 다른 풀이방법에는 뭐가 있을까 🧐

- `bitmask` : 대문자가 26개이니, 26 비트짜리 bitset를 만들고 해당 문자가 있으면 비트값을 1로 설정하여 푸는 방법
- `priority_queue` : 테스트케이스별로 우선순위 큐에 (알파벳수, 이름)을 저장해놓고, diffAlphabet()함수로 이름별로 알파벳 수를 저장해놓고 알파벳수가 가장 큰 것을 반환 + 알파벳 수가 같은 경우에 알파벳순서가 더 우선인 이름이 우선순위를 갖도록 하는 방법도 생각해보자
- `map` : 위의 우선순위 큐 방식과 비슷하다. 우선순위큐를 사용하지 않되 map을 사용하여 푸는 방법을 생각해보고 우선순위큐를 사용할 때와 어떤 차이가 있는지도 비교해보자

#### ⌨️ Small Dataset 코드 ⌨️

```c++
#include <iostream>
#include <vector>
using namespace std;

vector<bool> alphabet;

int diffAlphabet(const string& name) {
    alphabet = vector<bool>(26,false);
    int cnt;
    for(int a=0; a<name.length(); ++a) {
        if(name[a]==' ') continue;
        int val = name[a];
        if(!alphabet[val]) {
            alphabet[val] = true;
            cnt++;
        }
    }
    return cnt;
}

int main() {
    int T=0; int N=0;
    cin>>T;
    for(int t=0; t<T; ++t) {
        cin >> N; 
        int prev=0;
        string leader;
        for(int i=0; i<N; ++i) {
            string name;
            cin>>name;
            if(!i) {
                prev = diffAlphabet(name);
                leader = name;
            }
            else {
                int cur = diffAlphabet(name);
                if((prev < cur)||(prev == cur && leader[0]>name[0])) {
                    prev = cur;
                    leader = name;
                }
            }
        }
        cout<<"Case #"<<t+1<<":"<<leader<<endl;
    }
    return 0;
}
```

----

## Rain

#### ☑️ check-check ☑️

- [ ] 문제를 이해하였나
- [ ] 풀이 방법이 빨리 생각났나
- [ ] Small dataset을 통과하였나
- [ ] Large dataset을 통과하였나

#### 🙄 잘한 점, 아쉬웠던 점 🙄

- **잘한 점 **

- **아쉬웠던 점 **
  - 샘플 데이터를 보니 내가 이해한 문제 내용과 달랐다. 문제의 디테일한 부분을 이해 못했던 것 같다. 필요하다고 생각하는 부분만 읽지 말고, 모든 문장을 천천히 읽어보는 여유를 가져보자. 문제 속에 답이 있다. 
  - 이차원벡터에서 초기화하는 방법을 몰랐다.

#### 🧐 다른 풀이방법에는 뭐가 있을까 🧐

- 동적배열을 사용해도 되지만, 고정배열을 사용해도 되지 않을까. 서로 비교해보자

-----

## Jane's Flower Shop

#### ☑️ check-check ☑️

- [x] 문제를 이해하였나
- [ ] 풀이 방법이 빨리 생각났나
- [ ] Small dataset을 통과하였나
- [ ] Large dataset을 통과하였나

#### 🙄 잘한 점, 아쉬웠던 점 🙄

- **잘한 점 **

- **아쉬웠던 점 **
  - 문제는 이해했는데 다차원방정식을 어떻게 코드로 풀 지 몰랐다. 

#### 🧐 다른 풀이방법에는 뭐가 있을까 🧐

-----

## Clash Royale

#### ☑️ check-check ☑️

- [ ] 문제를 이해하였나
- [ ] 풀이 방법이 빨리 생각났나
- [ ] Small dataset을 통과하였나
- [ ] Large dataset을 통과하였나

#### 🙄 잘한 점, 아쉬웠던 점 🙄

- **잘한 점 **

- **아쉬웠던 점 **
  - 문제가 너무 어려웠다. 문제 이해 자체를 하지 못했다.

#### 🧐 다른 풀이방법에는 뭐가 있을까 🧐

----

## 문제 내용 

### Country Leader_problem

### Problem

The Constitution of a certain country states that the leader is the person with the name containing the greatest number of different alphabet letters. (The country uses the uppercase English alphabet from A through Z.) For example, the name `GOOGLE` has four different alphabet letters: E, G, L, and O. The name `APAC CODE JAM` has eight different letters. If the country only consists of these 2 persons, `APAC CODE JAM` would be the leader.

If there is a tie, the person whose name comes earliest in alphabetical order is the leader.

Given a list of names of the citizens of the country, can you determine who the leader is?

### Input

The first line of the input gives the number of test cases, **T**. **T** test cases follow. Each test case starts with a line with an interger **N**, the number of people in the country. Then **N** lines follow. The i-th line represents the name of the i-th person. Each name contains at most 20 characters and contains at least one alphabet letter.

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

| Input                                           | Output                                |
| ----------------------------------------------- | ------------------------------------- |
| 2<br/>3 <br/>ADAM <br/>BOB <br/>JOHNSON <br/>2 <br/>A AB C <br/>DEF    | Case #1: JOHNSON <br/>Case #2: A AB C |

In sample case #1, `JOHNSON` contains 5 different alphabet letters('H', 'J', 'N', 'O', 'S'), so he is the leader.

Sample case #2 would only appear in Large data set. The name `DEF` contains 3 different alphabet letters, the name `A AB C` also contains 3 different alphabet letters. `A AB C` comes alphabetically earlier so he is the leader.

-----

### Rain_problem

### Problem

There's an island in the sea. The island can be described as a matrix with **R** rows and **C** columns, with **H[i][j]** indicating the height of each unit cell. Following is an example of a 3*3 island:

```
3 5 5
5 4 5
5 5 5
```

Sometimes, a heavy rain falls evenly on every cell of this island. You can assume that an arbitrarily large amount of water falls. After such a heavy rain, some areas of the island (formed of one or more unit cells joined along edges) might collect water. This can only happen if, wherever a cell in that area shares an edge (not just a corner) with a cell outside of that area, the cell outside of that area has a larger height. (The surrounding sea counts as an infinite grid of cells with height 0.) Otherwise, water will always flow away into one or more of the neighboring areas (for our purposes, it doesn't matter which) and eventually out to sea. You may assume that the height of the sea never changes. We will use W[i][j] to denote the heights of the island's cells after a heavy rain. Here are the heights of the example island after a heavy rain. The cell with initial height 4 only borders cells with higher initial heights, so water will collect in it, raising its height to 5. After that, there are no more areas surrounded by higher cells, so no more water will collect. Again, note that water cannot flow directly between cells that intersect only at their corners; water must flow along shared edges.
Following is the height of the example island after rain:

```
3 5 5
5 5 5
5 5 5
```

Given the matrix of the island, can you calculate the total increased height sum(W[i][j]-**H[i][j]**) after a heavy rain?



### Input

The first line of the input gives the number of test cases, **T**. **T** test cases follow.
The first line of each test case contains two numbers **R** and **C** indicating the number of rows and columns of cells on the island. Then, there are **R** lines of **C** positive integers each. The j-th value on the i-th of these lines gives **H[i][j]**: the height of the cell in the i-th row and the j-th column.

### Output

For each test case, output one line containing `Case #x: y`, where `x` is the test case number (starting from 1) and `y` is the total increased height.

### Limits

1 ≤ **T** ≤ 100.
Time limit: 30 seconds per test set.
Memory limit: 1GB.
1 ≤ **H[i][j]** ≤ 1000.

#### Small dataset (Test set 1 - Visible)

1 ≤ **R** ≤ 10.
1 ≤ **C** ≤ 10.

#### Large dataset (Test set 2 - Hidden)

1 ≤ **R** ≤ 50.
1 ≤ **C** ≤ 50.

### Sample

| Input                                                        | Output                                |
| ------------------------------------------------------------ | ------------------------------------- |
| 3 <br/>3 3 <br/>3 5 5 <br/>5 4 5 <br/>5 5 5 <br/>4 4 <br/>5 5 5 1 <br/>5 1 1 5 <br/>5 1 5 5 <br/>5 2 5 8 <br/>4 3 <br/>2 2 2 <br/>2 1 2 <br/>2 1 2 <br/>2 1 2 | Case #1: 1 <br/>Case #2: 3 <br/>Case #3: 0 |

Case 1 is explained in the statement.

In case 2, the island looks like this after the rain:

```
5 5 5 1
5 2 2 5
5 2 5 5
5 2 5 8
```



Case 3 remains unchanged after the rain.

-----

### Jane's Flower Shop_problem

### Problem

Jane plans to open a flower shop in the local flower market. The initial cost includes the booth license, furnishings and decorations, a truck to transport flowers from the greenhouse to the shop, and so on. Jane will have to recoup these costs by earning income. She has estimated how much net income she will earn in each of the following **M** months.

Jane wants to predict how successful her flower shop will be by calculating the *IRR (Internal Rate of Return)* for the **M**-month period. Given a series of (time, cash flow) pairs (i, Ci), the IRR is the compound interest rate that would make total cash exactly 0 at the end of the last month. The higher the IRR is, the more successful the business is. If the IRR is lower than the inflation rate, it would be wise not to start the business in the first place.

For example, suppose the initial cost is $10,000 and the shop runs for 3 months, with net incomes of $3,000, $4,000, and $5,000, respectively. Then the IRR **r** is given by:

![img](https://codejam.googleapis.com/dashboard/get_file/AQj_6U1wKcglayr2tuMXOWvEcy_1QraaoZV3YgeMxqD_q4SwSiJMlGMCrNY/irr.png)

In this case, there is only one rate (~=8.8963%) that satisfies the equation.

Help Jane to calculate the IRR for her business. It is guaranteed that -1 < **r** < 1, and there is exactly one solution in each test case.

### Input

The first line of the input gives the number of test cases, **T**. **T** test cases follow. Each test case starts with a positive integer **M**: the number of months that the flower shop will be open. The next line contains **M** + 1 non-negative integers **Ci** (0 ≤ i ≤ **M**). Note that **C0** represents the initial cost, all the remaining **Ci**s are profits, the shop will always either make a positive net profit or zero net profit in each month, and will never have negative profits.

### Output

For each test case, output one line containing `Case #x: y`, where `x` is the test case number (starting from 1) and `y` is a floating-point number: the IRR of Jane's business. `y` will be considered correct if it is within an absolute or relative error of 10-6 of the correct answer. See the [FAQ](https://codingcompetitions.withgoogle.com/kickstart/faq) for an explanation of what that means, and what formats of real numbers we accept.

### Limits

1 ≤ **T** ≤ 100.
Time limit: 30 seconds per test set.
Memory limit: 1GB.
**C0** > 0.
0 ≤ **Ci** ≤ 1,000,000,000.

#### Small dataset (Test set 1 - Visible)

1 ≤ **M** ≤ 2.

#### Large dataset (Test set 2 - Hidden)

1 ≤ **M** ≤ 100.

### Sample

| Input                                                        | Output                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 3 <br/>2 <br/>200 100 100 <br/>3 <br/>10000 3000 4000 5000 <br/>5 <br/>3000 100 100 100 100 100   | Case #1: 0.000000000000 <br/>Case #2: 0.088963394693 <br/>Case #3: -0.401790748826 |

In sample case #1, the IRR is 0, Jane just paid back all the money and no interest.

Sample case #2 and #3 will only appear in large dataset.

----

### Clash Royale_problem

### Problem

Clash Royale is a real time strategy card game. Each card has an attack power and a level. Each player picks 8 cards to form a battle deck; the total attack power of a deck is the sum of the attack power of each of its cards. Players fight with each other by placing cards from their battle decks into the battle arena. The winner of a battle is rewarded with coins, which can be used to upgrade cards. Upgrading a card increases its attack power.



After days of arena fighting, Little Shawn has accumulated a total of **M** coins. He has decided to upgrade some of his cards. Little Shawn has **N** cards. The i-th card can have any level from 1 through **Ki**; the attack power for the j-th level is **Ai,j**. Cards must be upgraded one level at a time; the price to upgrade the i-th card from level j to level j+1 costs **Ci,j** coins. The i-th card is currently at level **Li** before Little Shawn has upgraded any cards.

Little Shawn wants to use some or all of his coins to upgrade cards, and then form a deck of exactly 8 cards, so that the deck's total attack power is as large as possible. Can you help him do this? He can upgrade the same card more than once as long as he can afford it, and he does not have to upgrade every card.

### Input

The first line of the input gives the number of test cases, **T**. **T** test cases follow. Each test case starts with 2 integers **M** and **N**, the number of coins and the number of cards that Little Shawn possesses. Then **N** blocks follow. The i-th block consists of 3 lines describing the i-th card. The first line contains two integers **Ki** and **Li**, the maximum possible level and current level of the card. The second line contains **Ki** integers **Ai,1**, **Ai,2**, ..., **Ai,Ki**, the attack power of each level. The third line contains **Ki**-1 integers **Ci,1**, **Ci,2**, ..., **Ci,Ki-1**, the number of coins required to upgrade a card that is currently at level 1, 2, ..., **Ki**-1.

### Output

For each test case, output one line containing `Case #x: y`, where `x` is the test case number (starting from 1) and `y` is the maximal possible total attack power of a deck that Little Shawn can form, using the coins that he has.

### Limits

Time limit: 60 seconds per test set.
Memory limit: 1GB.
1 ≤ **T** ≤ 100.
1 ≤ **Ki** ≤ 10.
1 ≤ **Li** ≤ **Ki**.
**Ai,j** < **Ai,j+1**.

#### Small dataset (Test set 1 - Visible)

1 ≤ **M** ≤ 1,000.
**N** = 8.
1 ≤ **Ai,j** ≤ 1,000.
1 ≤ **Ci,j** ≤ 1,000.

#### Large dataset (Test set 2 - Hidden)

1 ≤ **M** ≤ 1,000,000,000.
8 ≤ **N** ≤ 12.
1 ≤ **Ai,j** ≤ 1,000,000,000.
1 ≤ **Ci,j** ≤ 1,000,000,000.

### Sample

| Input                                                        | Output                        |
| ------------------------------------------------------------ | ----------------------------- |
| 2<br/>20 8<br/>3 1<br/>1 10 100<br/>1 2<br/>3 1<br/>1 10 100<br/>1 3<br/>3 1<br/>1 10 100<br/>1 4<br/>3 1<br/>1 10 100<br/>1 5<br/>3 1<br/>1 10 100<br/>1 6<br/>3 1<br/>1 10 100<br/>1 7<br/>3 1<br/>1 10 100<br/>1 8<br/>3 1<br/>1 10 100<br/>1 9<br/>30 10<br/>4 1<br/>1 10 100 200<br/>1 2 3<br/>3 1<br/>1 10 100<br/>2 4<br/>3 1<br/>1 10 100<br/>3 6<br/>4 2<br/>1 10 100 200<br/>4 8 16<br/>3 1<br/>1 10 100<br/>5 10<br/>3 1<br/>1 10 100<br/>6 12<br/>3 1<br/>1 10 100<br/>7 14<br/>3 1<br/>1 10 100<br/>8 16<br/>3 1<br/>1 10 100<br/>9 18<br/>3 1<br/>1 10 100<br/>10 20 | Case #1: 422<br/>Case #2: 504 |

In sample case #1, you can upgrade the first 4 cards to level 3, upgrade the 5th and 6th card to level 2, keep the last 2 cards level 1. This will cost you (1+2)+(1+3)+(1+4)+(1+5)+1+1=20 coins and the total attack power is 100+100+100+100+10+10+1+1=422 which is the maximal possible we can get.

Sample case #2 will only appear in large dataset.