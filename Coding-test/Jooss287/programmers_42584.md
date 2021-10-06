# 주식가격

[Programmers 42584 문제](https://programmers.co.kr/learn/courses/30/lessons/42584)  

> Stack/Deque 각 초당 변동되는 price의 가격에 따라 매 초 구입했을 시 이득이 -가 될 때 까지의 초를 구하는 문제입니다.

## 메모 할 사항

Vector를 이용하여 실제 데이터를 구성하고 deque를 이용해서 실제 데이터의 주소를 연결했습니다.

초기에 생각한 방법은 Stack, Deque 의 특성을 정확하게 사용하지 않고 pointer를 사용한 방법으로 효율성에서 모두 실패하는 결과를 보입니다.

Stack를 이용해서 top, pop의 O(1) 를 이용하여 문제를 풀었습니다.

## 입출력 예시

prices | return
|---|---|
[1,2,3,2,3] | [4,3,1,1,0]

## Result Code

```cpp
#include <string>
#include <vector>
#include <stack>
// #include <iostream>

using namespace std;

vector<int> solution(vector<int> prices) {
    vector<int> answer(prices.size(), 0);
    stack<pair<int, int>> stack_price;
    
    for(int i = 0; i < prices.size(); i++)
    {
        if (stack_price.empty())
            stack_price.push(make_pair(i, prices[i]));
        else
        {
            while( ( !stack_price.empty() && (stack_price.top().second > prices[i]) ) )
            {
                answer[stack_price.top().first] = i - stack_price.top().first;
                stack_price.pop();
            }
            stack_price.push(make_pair(i, prices[i]));
        }
    }
    
    while(!stack_price.empty())
    {
        answer[stack_price.top().first] = prices.size() - 1 - stack_price.top().first;
        stack_price.pop();
    }
    
    return answer;
}
```

### Result Code 테스트 결과

```text
정확성  테스트
테스트 1 〉 통과 (0.01ms, 3.7MB)
테스트 2 〉 통과 (0.03ms, 4.27MB)
테스트 3 〉 통과 (0.18ms, 4.34MB)
테스트 4 〉 통과 (0.17ms, 3.86MB)
테스트 5 〉 통과 (0.37ms, 4.32MB)
테스트 6 〉 통과 (0.02ms, 3.69MB)
테스트 7 〉 통과 (0.11ms, 4.26MB)
테스트 8 〉 통과 (0.24ms, 4.27MB)
테스트 9 〉 통과 (0.02ms, 3.69MB)
테스트 10 〉 통과 (0.21ms, 4.27MB)
효율성  테스트
테스트 1 〉 통과 (25.87ms, 24.3MB)
테스트 2 〉 통과 (18.96ms, 18.8MB)
테스트 3 〉 통과 (30.44ms, 26.9MB)
테스트 4 〉 통과 (22.65ms, 21.3MB)
테스트 5 〉 통과 (15.60ms, 16.3MB)
```

## 초기 작성한 코드

```cpp
#include <string>
#include <vector>
#include <deque>
#include <iostream>

using namespace std;

vector<int> solution(vector<int> prices) {
    vector<int> answer(prices.size(), 0);
    deque<vector<int*>> stockDeque;
    
    for(int i = 0; i < prices.size(); i++)
    {
        for (auto& stock_time : stockDeque)
        {
            *(stock_time[1]) += 1;
        }
        
        deque<vector<int*>>::iterator itr = stockDeque.begin();
        while(itr != stockDeque.end())
        {
            if ( *((*itr)[0]) > prices[i])
            {
                stockDeque.erase(itr);
            }
            else
                itr++;
        }
        
        vector<int*> temp;
        temp.push_back(&prices[i]);
        temp.push_back(&answer[i]);
        stockDeque.push_back(temp);
    }
    return answer;
}
```

### 초기테스트

```text
정확성  테스트
테스트 1 〉 통과 (0.01ms, 3.66MB)
테스트 2 〉 통과 (0.04ms, 4.27MB)
테스트 3 〉 통과 (0.26ms, 3.93MB)
테스트 4 〉 실패 (signal: aborted (core dumped))
테스트 5 〉 실패 (signal: aborted (core dumped))
테스트 6 〉 통과 (0.02ms, 4.34MB)
테스트 7 〉 실패 (signal: aborted (core dumped))
테스트 8 〉 통과 (0.20ms, 3.79MB)
테스트 9 〉 통과 (0.02ms, 4.32MB)
테스트 10 〉 통과 (0.34ms, 3.81MB)
효율성  테스트
테스트 1 〉 실패 (signal: aborted (core dumped))
테스트 2 〉 실패 (signal: aborted (core dumped))
테스트 3 〉 실패 (signal: aborted (core dumped))
테스트 4 〉 실패 (signal: aborted (core dumped))
테스트 5 〉 실패 (signal: aborted (core dumped))
```
