# 전화번호 목록
[Programmers 42577 문제](https://programmers.co.kr/learn/courses/30/lessons/42577#)  


## 메모 할 사항
전화번호 목록이 제공되며, 그 중 접두어가 같은 번호가 하나라도 있는가를 판별하는 문제입니다.  
간단히 Algorithm 헤더의 sort기능을 사용하여 목록을 정렬한 뒤, 순서대로 비교하는 방식을 선택했습니다.
너무 sort 기능에 의존하는 것 같아 다른 방식의 정렬 혹은 sort 기능 없이 유사한 결과를 찾는 경우를 연구해봐야 할 것 같습니다.  
본래 문제 보기에서는 bool answer = true; 이후 answer를 반환하는 형식으로 되어 있었지만 큰 문제가 되지 않을 것 같아 바로 false 혹은 true를 반환하도록 하였습니다.
  
여담으로 예전 string 관련 함수를 하나도 모를 때는 string을 배열형태로 한문자 한문자 비교 진행한 적이 있었는데, 함수 하나를 알고 모르고가 코딩의 쾌적도를 바꾸는 것 같습니다. 본 문제에서는 string의 substr함수를 사용해 비교했습니다.

## 입출력 예시
phone_book | return
|---|---|
[119, 97674223, 1195524421] | false
[123,456,789] | true
[12,123,1235,567,88] | false


## Result Code

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool solution(vector<string> phone_book) {
    sort(phone_book.begin(), phone_book.end());
    for(int i = 0; i < phone_book.size() - 1; i++)
    {
        if(phone_book[i] == phone_book[i + 1].substr(0, phone_book[i].size()))
            return false;
    }
    return true;
}
```

# 성능 및 결과
```
정확성  테스트
테스트 1 〉	통과 (0.01ms, 3.96MB)
테스트 2 〉	통과 (0.01ms, 3.93MB)
테스트 3 〉	통과 (0.01ms, 3.94MB)
테스트 4 〉	통과 (0.01ms, 3.93MB)
테스트 5 〉	통과 (0.01ms, 3.96MB)
테스트 6 〉	통과 (0.01ms, 3.79MB)
테스트 7 〉	통과 (0.01ms, 3.95MB)
테스트 8 〉	통과 (0.01ms, 3.96MB)
테스트 9 〉	통과 (0.01ms, 3.95MB)
테스트 10 〉	통과 (0.01ms, 3.97MB)
테스트 11 〉	통과 (0.01ms, 3.98MB)
효율성  테스트
테스트 1 〉	통과 (3.50ms, 4.57MB)
테스트 2 〉	통과 (3.62ms, 4.57MB)
채점 결과
정확성: 84.6
효율성: 15.4
합계: 100.0 / 100.0
```





