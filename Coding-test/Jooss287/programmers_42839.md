# 소수 찾기

[Programmers 42839 문제](https://programmers.co.kr/learn/courses/30/lessons/42839)  

> 완전탐색 문제로 제시된 숫자의 조합 중 소수를 찾아 소수의 개수를 추출하는 문제입니다.

## 메모 할 사항

string의 나열을 사용하여 문제를 풀려고 했습니다. 문자열 개수만큼 반복시키는 방법인데 메모리 초과로 인해 다른 알고리즘을 찾아야 했습니다. 과도한 시간 소모로 인해 어쩔 수 없이 다른 방법을 서치하여 학습하는 방식을 사용하였습니다.

1. Next_permunation 사용하는 방법
2. 가장 큰 수 구해서 아래의 모든 소수를 구하는 방법 (문자열 나열)

결국 주어진 문자열을 모두 나열시키는 방법에 대해서 근본적인 고민이 필요해 보입니다.  
차후에 다시 고민 후 해결 필요

___

1년이 지난 시점 다시 풀어보았습니다. 간단한 string재귀함수를 이용하여 모든 string을 나열하고 숫자로 변환시켜 소수판단을 진행했습니다.
PrimeNumber를 vector를 사용하여 저장하고 erase(unique)를 사용하여 제거하려고 하였으나 잘 안되는 모습에 map을 사용하여 데이터를 저장하고, 혹시 모를 0을 제거하였습니다.

## 입출력 예시

numbers | return
|---|---|---|
17 | 3
011 | 2

## Result Code

```cpp
#include <string>
#include <vector>
#include <cmath>
#include <set>
#include <algorithm>
#include <iostream>
#include <map>

using namespace std;

bool isPrime(int number)
{
    int PrimeCount = ((int)sqrt(number) + 1);
    
    if ( number == 1)
        return false;
    
    for( int i = 2; i < PrimeCount; i++)
    {
        if ( (number % i ) == 0)
        {
            return false;
        }
    }
    
    return true;
}

void findPrimeNumber(string numbers, string combineNumber, int stairs, map<int,bool> &primeNumberCnt)
{
    stairs++;
    for(int i = 0; i < numbers.size(); i++)
    {
        string tempStr(numbers);
        string combineNum(combineNumber);
        char numChar = numbers[i];
        tempStr.erase(i,1);
        combineNum.push_back(numChar);
        
        long num = atoi(combineNum.c_str());
        if (isPrime(num))
        {
            primeNumberCnt.insert(make_pair(num,true));
            cout << num << " is ";
            cout << "true\n";
        }
            
        
        findPrimeNumber(tempStr, combineNum, stairs, primeNumberCnt);
    }
    
    
}

int solution(string numbers) {
    string combineNum;
    int stairs = 0;
    map<int, bool> primeNumberCnt;
    
    findPrimeNumber(numbers, combineNum, stairs, primeNumberCnt);
    primeNumberCnt.erase(0);
    
    return primeNumberCnt.size();
}

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

## 초기테스트

```text
메모리 오버, 테스트 불가
```
