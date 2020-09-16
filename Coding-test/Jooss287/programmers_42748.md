# 전화번호 목록
[Programmers 42748 문제](https://programmers.co.kr/learn/courses/30/lessons/42748)  

> K번째 숫자를 추출 하는 문제입니다.

## 메모 할 사항
문제 자체는 매우 간단했으나 Visual studio IDE처럼 자동완성 기능에 익숙해 진 까닭에 자동완성이 없어 에러고치는데 시간을 소요했습니다.

## 입출력 예시

array | commands | return |
|---|---|---|
[1, 5, 2, 6, 3, 7, 4] | [[2, 5, 3], [4, 4, 1], [1, 7, 3]] | [5, 6, 3]



## Result Code

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> array, vector<vector<int>> commands) {
    vector<int> answer;
    
    for ( vector<vector<int>>::iterator itr = commands.begin(); itr != commands.end(); itr++)
    {
        vector<int> cmd = *itr;
        
        vector<int> target(array.begin()+cmd[0]-1, array.begin()+cmd[1]);
        sort(target.begin(), target.end());
        answer.push_back(target[cmd[2]-1]);
    }
        
    return answer;
}
```

# 성능 비교
## 초기테스트
```
정확성  테스트
테스트 1 〉	통과 (0.01ms, 3.93MB)
테스트 2 〉	통과 (0.01ms, 3.97MB)
테스트 3 〉	통과 (0.01ms, 3.83MB)
테스트 4 〉	통과 (0.01ms, 3.95MB)
테스트 5 〉	통과 (0.01ms, 3.95MB)
테스트 6 〉	통과 (0.01ms, 3.97MB)
테스트 7 〉	통과 (0.01ms, 3.77MB)
채점 결과
정확성: 100.0
합계: 100.0 / 100.0
```



