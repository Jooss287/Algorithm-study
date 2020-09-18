# 가장 큰 수
[Programmers 42746 문제](https://programmers.co.kr/learn/courses/30/lessons/42746)  

> 0 이상의 양의 정수가 주어 질 때, 숫자를 이어 붙여 가장 큰 문자열을 만드는 문제입니다.

## 메모 할 사항
일반적인 예외처리로는 한계에 봉착했습니다. 이러한 알고리즘 문제는 예외처리보다는 문제의 핵심을 파악하려 노력해야 합니다.  
하루종일 고민 한 결과 문제를 풀기 위한 기본적인 알고리즘 지식이 필요하다고 판단하여 인터넷을 검색하여 어느정도의 답을 검색하였습니다. Int를 문자화시켜 4자리수가 될때까지 반복시켜서 비교합니다. 0에 대한 예외처리를 하여 마무리 합니다.

## 입출력 예시

numbers | return
|---|---|---|
[6, 10, 2] | 6210
[3, 30, 34, 5, 9] | 9534330


## Result Code

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <cmath>

using namespace std;

bool UserSort(int a, int b);
string ConvertToStr(int item);

string solution(vector<int> numbers) {
    string answer = "";
    vector<string> numString;
    
    sort(numbers.begin(), numbers.end(), UserSort);
    for ( auto item : numbers)
    {
        string itemStr = "";
        if ( !( ( answer == "") && ( item == 0 ) ) )
            itemStr = to_string(item);
        answer += itemStr;
    }
    if (answer.compare("") == 0)
        answer = "0";
    
    return answer;
}

bool UserSort(int a, int b)
{
    return ConvertToStr(a) > ConvertToStr(b);
}

string ConvertToStr(int item)
{
    string text = to_string(item);
    int inx = 0;
    while ( text.size() < 4)
    {
        text = text + text.at(inx++);
    }
    return text;
}
```

# 성능 비교
## 초기테스트
```
정확성  테스트
테스트 1 〉	통과 (206.91ms, 6.54MB)
테스트 2 〉	통과 (101.75ms, 5.14MB)
테스트 3 〉	통과 (278.40ms, 7.66MB)
테스트 4 〉	통과 (4.99ms, 3.79MB)
테스트 5 〉	통과 (164.92ms, 6.25MB)
테스트 6 〉	통과 (156.30ms, 5.91MB)
테스트 7 〉	통과 (0.04ms, 3.97MB)
테스트 8 〉	통과 (0.03ms, 3.95MB)
테스트 9 〉	통과 (0.03ms, 3.95MB)
테스트 10 〉	통과 (0.03ms, 3.9MB)
테스트 11 〉	통과 (0.06ms, 3.98MB)
채점 결과
정확성: 100.0
합계: 100.0 / 100.0
```



