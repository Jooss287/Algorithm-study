# 완주하지 못한 선수
[Programmers 42576 문제](https://programmers.co.kr/learn/courses/30/lessons/42576#)  
  
  
## 메모 할 사항
 아직 자료구조를 이론적으로 제대로 배운적이 없기 때문에 이후 map, hash 등의 공부와,  
 특히 어떤 상황에서 어떤 것이 효율적인지에 대한 구현 경험 필요  
   
 - 이 문제의 경우 이전에 다른 문제를 풀 때 vector와 sort를 활용한 경험이 있어 우선적으로 사용  
 sort를 사용해 각 배열을 정렬시킨 뒤 순서대로 비교하다보면 참여자와 완주자가 다른 순간이 생기며,  
 이 경우 해당 참여자가 완주자의 명단에 없는 것이 되기 때문에 검출 가능  

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
#include <algorithm>
using namespace std;

string solution(vector<string> participant, vector<string> completion) {

    std::sort(participant.begin(), participant.end());
    std::sort(completion.begin(),completion.end());
    
    for(int i = 0 ; i <= participant.size(); i++)
    {
        if(participant[i] != completion[i])
        {
            return participant[i];
        }
    } 
}
```
  
#성능 및 결과
```
정확성  테스트
테스트 1 〉	통과 (0.01ms, 3.96MB)
테스트 2 〉	통과 (0.01ms, 3.94MB)
테스트 3 〉	통과 (0.28ms, 3.94MB)
테스트 4 〉	통과 (0.57ms, 3.95MB)
테스트 5 〉	통과 (0.59ms, 3.93MB)
효율성  테스트
테스트 1 〉	통과 (37.63ms, 14.2MB)
테스트 2 〉	통과 (57.57ms, 19.6MB)
테스트 3 〉	통과 (71.81ms, 23.2MB)
테스트 4 〉	통과 (79.35ms, 25.3MB)
테스트 5 〉	통과 (77.01ms, 25.3MB)
채점 결과
정확성: 50.0
효율성: 50.0
합계: 100.0 / 100.0
```
