# 완주하지 못한 선수
[Programmers 42577 문제](https://programmers.co.kr/learn/courses/30/lessons/42577#)  

> Hash 를 사용한 문제로 접두어를 판단하여 접두어 중복이 존재 할 시 false를 추려 내는 문제입니다.

## 메모 할 사항


## 입출력 예시
phone_book | return
|---|---|
[123,456,789] | true
[12,123,1235,567,88] | false


## Result Code

```cpp
#include <string>
#include <vector>
#include <map>
#include <set>
#include <cstring>

using namespace std;

bool solution(vector<string> phone_book) {
    map<int, set<string>> book;
    for ( int i = 0; i < phone_book.size(); i++)
    {
        book[phone_book[i].size()].insert(phone_book[i]);
    }
    
    for ( int i = 0; i < phone_book.size(); i++)
    {
        for ( map<int, set<string>>::iterator itr = book.begin(); itr != book.end(); itr++)
        {
            if ( itr->first >= phone_book[i].size())
                break;
            
            set<string> same_size_list = itr->second;
            for ( set<string>::iterator itr_set = same_size_list.begin(); itr_set != same_size_list.end(); itr_set++)
            {
                if ( phone_book[i] == *itr_set )
                    continue;
                
                if ( phone_book[i].find(*itr_set) )
                {
                    return false;
                }
            }
        }
    }
    return true;
}
```

# 성능 비교
## 초기테스트
```
정확성  테스트
테스트 1 〉	실패 (0.02ms, 3.97MB)
테스트 2 〉	통과 (0.01ms, 3.93MB)
테스트 3 〉	통과 (0.02ms, 3.93MB)
테스트 4 〉	통과 (0.02ms, 3.96MB)
테스트 5 〉	실패 (0.02ms, 3.96MB)
테스트 6 〉	실패 (0.01ms, 3.99MB)
테스트 7 〉	실패 (0.01ms, 3.96MB)
테스트 8 〉	통과 (0.02ms, 3.96MB)
테스트 9 〉	통과 (0.01ms, 3.98MB)
테스트 10 〉	통과 (0.01ms, 3.98MB)
테스트 11 〉	실패 (0.01ms, 3.96MB)
효율성  테스트
테스트 1 〉	통과 (4.01ms, 5.3MB)
테스트 2 〉	통과 (4.12ms, 5.15MB)
채점 결과
정확성: 46.2
효율성: 15.4
합계: 61.5 / 100.0
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





