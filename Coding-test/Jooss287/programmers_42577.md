# 전화번호 목록
[Programmers 42577 문제](https://programmers.co.kr/learn/courses/30/lessons/42577#)  

> 전화번호부에서 한 전화번호가 다른 번호의 __접두어__를 판단하여 접두어 중복이 존재 할 시 false를 추려 내는 문제입니다.

## 메모 할 사항
처음에 ```접두어```를 신경 쓰지 않고 ```포함```의 의미로 접근하여 테스트에서 실패케이스가 발생하였습니다.  
Find 알고리즘 대신 Substr을 사용하여 접두어로 비교하여 문제를 통과 할 수 있었습니다.  
```CString```에 익숙해 져 있어서 STL의 ```string```에 익숙해 질 필요가 있습니다.
* string.substr(start_index, start_index+count): 같을 시 0

먼저 map<int, set<string>>을 사용하여 ```phone_book```을 size별로 나누어 정리합니다, 이 때 set으로 같은 size의 string 데이터를 정렬 해 줍니다. 입력 데이터를 for구문으로 돌려 주면서 자기 자신보다 같거나 작은 size를 돌면서 접두어 비교를 진행합니다.

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

## 수정 후 테스트
```
채점을 시작합니다.
정확성  테스트
테스트 1 〉	통과 (0.02ms, 3.96MB)
테스트 2 〉	통과 (0.01ms, 3.97MB)
테스트 3 〉	통과 (0.02ms, 3.89MB)
테스트 4 〉	통과 (0.01ms, 3.96MB)
테스트 5 〉	통과 (0.02ms, 3.97MB)
테스트 6 〉	통과 (0.01ms, 3.97MB)
테스트 7 〉	통과 (0.01ms, 3.96MB)
테스트 8 〉	통과 (0.01ms, 3.72MB)
테스트 9 〉	통과 (0.01ms, 3.78MB)
테스트 10 〉	통과 (0.01ms, 3.92MB)
테스트 11 〉	통과 (0.02ms, 3.96MB)
효율성  테스트
테스트 1 〉	통과 (4.09ms, 5.32MB)
테스트 2 〉	통과 (3.76ms, 5.15MB)
채점 결과
정확성: 84.6
효율성: 15.4
합계: 100.0 / 100.0
```





