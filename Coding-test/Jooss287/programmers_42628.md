# 이중우선순위큐

[Programmers 42628 문제](https://programmers.co.kr/learn/courses/30/lessons/42628)  

> Hash 문제로, 주어진 명령어를 통해 최대, 최소값을 구하는 문제입니다.

## 메모 할 사항

중복 가능한 단일 값이므로 multiset을 통하여 계산하였고, 별도의 정렬을 사용하지 않았습니다.

## 입출력 예시

operations | return
|---|---|
["I 16","D 1"] | [0,0]
["I 7","I 5","I -5","D -1"] | [7,5]

## Result Code

```cpp
void parseOperations(string operations, string &cmd, int &value)
{
    int sp = operations.find(" ");
    cmd = operations.substr(0, sp);
    string temp = operations.erase(0, sp+1);
    value = stoi(temp);
}


vector<int> solution(vector<string> operations) {
    vector<int> answer;
    multiset<int> q;

    for(auto& op : operations)
    {
        string cmd;
        int value;
        parseOperations(op, cmd, value);

        if ( cmd.compare("I") == 0 )
        {
            q.insert(value);
        }
        else
        {
            if ( q.empty() )
                continue;
            if ( value > 0 )
            {
                q.erase(*(q.rbegin()));
            }
                
            else
                q.erase(*(q.begin()));
        }
    }

    if ( q.empty() )
    {
        answer.push_back(0);
        answer.push_back(0);
    }
    else
    {
        answer.push_back(*(q.rbegin()));
        answer.push_back(*(q.begin()));
    }
    return answer;
}
```

### Result Code 테스트 결과

```text
정확성  테스트
테스트 1 〉통과 (0.02ms, 3.67MB)
테스트 2 〉통과 (0.02ms, 3.64MB)
테스트 3 〉통과 (0.03ms, 3.69MB)
테스트 4 〉통과 (0.02ms, 4.31MB)
테스트 5 〉통과 (0.02ms, 4.26MB)
테스트 6 〉통과 (0.04ms, 4.31MB)
```

## 초기 작성한 코드

```cpp

```

### 초기테스트

```text
```
