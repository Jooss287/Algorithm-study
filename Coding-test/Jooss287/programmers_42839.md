# 소수 찾기
[Programmers 42839 문제](https://programmers.co.kr/learn/courses/30/lessons/42839)  

> 완전탐색 문제로 제시된 숫자의 조합 중 소수를 찾아 소수의 개수를 추출하는 문제입니다.

## 메모 할 사항
string의 나열을 사용하여 문제를 풀려고 했습니다. 문자열 개수만큼 반복시키는 방법인데 메모리 초과로 인해 다른 알고리즘을 찾아야 했습니다. 과도한 시간 소모로 인해 어쩔 수 없이 다른 방법을 서치하여 학습하는 방식을 사용하였습니다.

1. Next_permunation 사용하는 방법
2. 가장 큰 수 구해서 아래의 모든 소수를 구하는 방법 (문자열 나열)

결국 주어진 문자열을 모두 나열시키는 방법에 대해서 근본적인 고민이 필요해 보입니다.  
차후에 다시 고민 후 해결 필요

## 입출력 예시

numbers | return
|---|---|---|
17 | 3
011 | 2


## Result Code

```cpp

```

## 초기 작성한 코드
```cpp
#include <string>
#include <vector>
#include <cmath>

#include <iostream>

using namespace std;

int solution(string numbers) {
    int answer = 0;
    vector<string> numbers_array;
    
    numbers += '-';
    for ( int i=0; i < numbers.size(); i++)
    {
        string temp;
        temp += numbers.at(i);
        numbers_array.push_back(temp);
    }
        
    
    //문자열 조합 구하기
    int index = 1;
    while ( index != numbers.size() )
    {
        cout << index << endl;
        vector<string> temp_number;
        for ( int i = 0; i < numbers.size(); i++)
        {
            for( string num_str : numbers_array)
            {
                string num = num_str + numbers[i];
                temp_number.push_back(num);
            }
        }
        numbers_array = temp_number;
    }
    
    
    for( string num : numbers_array)
    {
        cout << num << endl;
        num.replace('-');
        answer += IsPrime(stoi(num));
    }
    return answer;
}

bool IsPrime(int number)
{
    int PrimeCount = ((int)sqrt(number) + 1);
    
    for( int i = 2; i < PrimeCount; i++)
    {
        if ( (number % i ) != 0)
        {
            return false;
        }
    }
    
    return true;
}
```

# 성능 비교
## 초기테스트
```
메모리 오버, 테스트 불가
```

## 알고리즘 변경 후
```
```


