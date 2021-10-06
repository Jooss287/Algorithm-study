# 큰 수 만들기

[Programmers 42883 문제](https://programmers.co.kr/learn/courses/30/lessons/42883)  

> 탐욕법(Greed) 숫자로 된 문자열에서 숫자 n개를 빼서 가장 큰 수를 만드는 문제입니다.

## 메모 할 사항

나열된 문자열에서 앞에서부터 두 수를 확인하여 앞의 수가 더 작으면 삭제하는 방법을 사용했습니다. n개 삭제하면 반복을 종료합니다.

* Erase했을 시에 처리해야 할 조건들을 다시 한번 생각합니다.
* 변수들이 조건을 빠져나가는 상황을 잘 생각합니다.

## 입출력 예시

number | k | return
|---|---|---|
"1294" | 2 | "94"
"1231234" | 3 | "3234"
"4177252841" | 4 | "775841"

## Result Code

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

string solution(string number, int k) {
    int numberPt = 1;
    
    while(1)
    {
        if ( number[numberPt-1] < number[numberPt])
        {
            number.erase(numberPt-1,1);
            k--;
            if ( numberPt > 1)
                numberPt--;
        }
        else
        {
            numberPt++;
        }

        if ( k <= 0)
            break;
        if ( numberPt >= number.size() )
        {
            for( int i = 0; i < k; i++)
                 number.pop_back();
            break;
        }
    }
    return number;
}
```

### Result Code 테스트 결과

```text
테스트 1 〉 통과 (0.01ms, 3.75MB)
테스트 2 〉 통과 (0.01ms, 3.75MB)
테스트 3 〉 통과 (0.01ms, 4.39MB)
테스트 4 〉 통과 (0.02ms, 4MB)
테스트 5 〉 통과 (0.03ms, 3.81MB)
테스트 6 〉 통과 (1.18ms, 3.75MB)
테스트 7 〉 통과 (9.62ms, 3.99MB)
테스트 8 〉 통과 (56.26ms, 3.79MB)
테스트 9 〉 통과 (2.92ms, 5.3MB)
테스트 10 〉 통과 (1624.46ms, 5.65MB)
테스트 11 〉 통과 (0.01ms, 3.75MB)
테스트 12 〉 통과 (0.01ms, 3.97MB)
```

## 초기 작성한 코드

```cpp

```

### 초기테스트

```text
```
