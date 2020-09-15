# 완주하지 못한 선수
[Programmers 42576 문제](https://programmers.co.kr/learn/courses/30/lessons/42576#)  

> Hash 를 사용한 문제로 참여자와 완주자를 비교하여 완주하지 못한 한명을 추려내는 문제입니다.

## 메모 할 사항
c++에서 Dictionary 자료구조는 map을 사용합니다.  
```map``` 는 Balanced tree로 되어 있고 그 중에서도 red-block트리로 구현되어 있습니다.  
```unordered_map```는 hash table로 구현되어 있습니다.  
두 가지 중에서 지금 사용하는 알고리즘은 order가 필요가 없습니다. 그러므로 unordred_map을 사용하여 속도를 조금 더 올려 줍니다.

## 입출력 예시
participant | completion | return
---|---|---
[leo, kiki, eden] | [eden, kiki] | leo
[marina, josipa, nikola, vinko, filipa] | [josipa, filipa, marina, nikola] | vinko
[mislav, stanko, mislav, ana] | [stanko, ana, mislav] | mislav


## Result Code

```cpp
#include <string>
#include <vector>
#include <unordered_map>

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    string answer = "";
    
    unordered_map<string, int> result;
    
    for( int i = 0; i < completion.size(); i++)
    {
        result[completion[i]]--;
        result[participant[i]]++;
    }
    result[participant[participant.size()-1]]++;
    
    
    for(unordered_map<string,int>::iterator itr = result.begin(); itr != result.end(); itr++)
    {
        if ( itr->second > 0) {
            answer = itr->first;
            break;
        }
    }

    return answer;
}
```

# 성능 비교
## map
```
채점을 시작합니다.
정확성  테스트
테스트 1 〉	통과 (0.01ms, 3.98MB)
테스트 2 〉	통과 (0.01ms, 3.96MB)
테스트 3 〉	통과 (0.36ms, 3.96MB)
테스트 4 〉	통과 (0.77ms, 3.96MB)
테스트 5 〉	통과 (0.74ms, 3.97MB)
효율성  테스트
테스트 1 〉	통과 (56.22ms, 18.2MB)
테스트 2 〉	통과 (76.80ms, 25.4MB)
테스트 3 〉	통과 (112.04ms, 30.3MB)
테스트 4 〉	통과 (125.85ms, 32.8MB)
테스트 5 〉	통과 (111.00ms, 32.9MB)
채점 결과
정확성: 50.0
효율성: 50.0
합계: 100.0 / 100.0
```

## unordered_map
```
채점을 시작합니다.
정확성  테스트
테스트 1 〉	통과 (0.01ms, 3.96MB)
테스트 2 〉	통과 (0.01ms, 3.91MB)
테스트 3 〉	통과 (0.18ms, 3.97MB)
테스트 4 〉	통과 (0.32ms, 3.97MB)
테스트 5 〉	통과 (0.35ms, 3.95MB)
효율성  테스트
테스트 1 〉	통과 (19.81ms, 17.8MB)
테스트 2 〉	통과 (31.53ms, 25.4MB)
테스트 3 〉	통과 (36.23ms, 29.9MB)
테스트 4 〉	통과 (40.89ms, 32.5MB)
테스트 5 〉	통과 (42.27ms, 32.5MB)
채점 결과
정확성: 50.0
효율성: 50.0
합계: 100.0 / 100.0
```