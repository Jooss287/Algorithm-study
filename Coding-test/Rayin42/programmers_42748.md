# 전화번호 목록
[Programmers 42748 문제](https://programmers.co.kr/learn/courses/30/lessons/42748)  

> 배열을 입력받은 범위만큼 슬라이스 한 뒤 정렬, K번째 숫자를 추출 하는 문제입니다.

## 메모 할 사항
정렬과 k번째 수를 찾는 것은 쉬운 문제로, 입력받은 범위만큼 배열을 추출해 내는 방법을 고민했습니다.

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
    for (int i = 0; i < commands.size(); i++)
    {
        vector<int> copy;
        for (int j = commands[i][0] - 1; j < commands[i][1]; j++)
        {
            copy.push_back(array[j]);
        }
        sort(copy.begin(), copy.end());
        answer.push_back(copy[commands[i][2] - 1]);
    }
    return answer;
}
```

# 성능 비교
## 초기테스트
```
정확성  테스트
테스트 1 〉	통과 (0.01ms, 3.96MB)
테스트 2 〉	통과 (0.01ms, 3.96MB)
테스트 3 〉	통과 (0.01ms, 3.96MB)
테스트 4 〉	통과 (0.01ms, 3.9MB)
테스트 5 〉	통과 (0.01ms, 3.96MB)
테스트 6 〉	통과 (0.01ms, 3.93MB)
테스트 7 〉	통과 (0.01ms, 3.96MB)
채점 결과
정확성: 100.0
합계: 100.0 / 100.0
```



