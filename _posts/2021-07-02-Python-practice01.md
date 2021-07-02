---
layout: post
title: Python algorithm Practice 01 "Divide and Conquer"
subtitle: algorithm practice "Divide and Conquer"
categories: [Python]
tags: [python, practice, algorithm]
comments: true
---

## Divide and Conquer (Merge sort, min max 찾기)

Divide and Conquer (분할정복법)은 주어진 문제를 작은 Problem으로 나누고 작은 Problem들을 해결하여 정복하는 방법입니다.

나눈 작은 Problem의 해답을 얻을 수 있으면 답을 구하고 그렇지 않으면 더 작은 Problem으로 다시 나눠줍니다.

즉 답을 구할 수 있는 만큼 충분히 Problem을 나눠주고 답을 구하는 방법입니다.

<br/>

### Divide and Conquer Algorithm 전략
  - 전체 Problem을 여러 작은 Problem들로 분할해줍니다.
  - 분할(Divide)된 Problem들을 각각 정복(Conquer)해줍니다. 
  - 작은 Problem을 통해 얻은 해답을 통합하여 원래의 Problem을 해결합니다.
  
<br/>

#### Divide and Conquer를 통한 최대값, 최솟값 찾기
```python3
 def divide_conquer(n):
     if len(n) <= 1:                     # list n의 크기가 1이면 return해줍니다.
         return n
     mid = len(n) // 2                   #len(n)/2 를 해주어 mid 변수에 저장해줍니다.
     left = n[:mid]                      #list n에서 첫번째부터 mid 전 까지 left로 저장해줍니다. 
     right = n[mid:]                     #list n에서 mid부터 마지막까지 right로 저장해줍니다.
     left = divide_conquer(left)         #recursion을 이용하여 왼쪽list를 다시 반으로 나눕니다.
     right = divide_conquer(right)       #recursion을 이용하여 오른쪽list를 다시 반으로 나눕니다.
     return conquer(left, right)         # 함수 conquer로 이동하여줍니다.

 def conquer(L, R):
     result = []                         #정렬된 값을 저장할 list를 만들어줍니다.
     while len(L) > 0 or len(R) > 0:     #L과R의 list가 모두 사용될 때 까지 반복해줍니다.
         if len(L) > 0 and len(R) > 0:   #L과R list에 값이 모두 남아있다면
             if L[0] <= R[0]:            #만약 L[0]값이 R[0]보다 작다면 
                 result.append(L[0])     #결과값에 L[0]을 추가해줍니다.
                 L = L[1:]               #그리고 L[0]는 제거해주고 앞으로 한칸씩 당겨줍니다.
             else:                       #반대 라면
                 result.append(R[0])     #결과값에 R[0]을 추가해줍니다.
                 R = R[1:]               #그리고 R[0]는 제거해주고 앞으로 한칸씩 당겨줍니다.
         elif len(L) > 0:                #만약 L list에 값만 남았다면
             result.append(L[0])         #L list 자체는 sort가 되있으므로 
             L = L[1:]                   #결과값에 순서대로 넣어줍니다.   
         elif len(R) > 0:                #만약 R list에 값만 남았다면
             result.append(R[0])         #R list 자체는 sort가 되있으므로
             R = R[1:]                   #결과값에 순서대로 넣어줍니다.
     return minmax(result)               #최종 결과값을 minmax 함수로 이동시켜줍니다.

 def minmax(n):                          #최종 결과값은 오름차순으로 정렬되어있기 때문에
     my_min = n[0]                       #최솟값은 0번째에 위치하고
     my_max = n[-1]                      #최대값은 -1번째에 위치할것 입니다.
     return my_min, my_max               #이들을 뽑아준 뒤 return하여 줍니다.

 l = [3,8,5,7,6,1,2,9,11]
 print("(Min,Max)=",divide_conquer(l))
 
```

<br/>

#### Divide and Conquer를 통한 Merge Sort 알고리즘
```python3
def mergesort(n):
    if len(n) <= 1:                     # list n의 크기가 1이면 return해줍니다.
        return n
    mid = len(n) // 2                   #len(n)/2 를 해주어 mid 변수에 저장해줍니다.
    left = n[:mid]                      #list n에서 첫번째부터 mid 전 까지 left로 저장해줍니다. 
    right = n[mid:]                     #list n에서 mid부터 마지막까지 right로 저장해줍니다.
    left = mergesort(left)              #recursion을 이용하여 왼쪽list를 다시 반으로 나눕니다.
    right = mergesort(right)            #recursion을 이용하여 오른쪽list를 다시 반으로 나눕니다.
    return conquer(left, right)         # 함수 conquer로 이동하여줍니다.

def conquer(L, R):
    result = []                         #정렬된 값을 저장할 list를 만들어줍니다.
    while len(L) > 0 or len(R) > 0:     #L과R의 list가 모두 사용될 때 까지 반복해줍니다.
        if len(L) > 0 and len(R) > 0:   #L과R list에 값이 모두 남아있다면
            if L[0] <= R[0]:            #만약 L[0]값이 R[0]보다 작다면 
                result.append(L[0])     #결과값에 L[0]을 추가해줍니다.
                L = L[1:]               #그리고 L[0]는 제거해주고 앞으로 한칸씩 당겨줍니다.
            else:                       #반대 라면
                result.append(R[0])     #결과값에 R[0]을 추가해줍니다.
                R = R[1:]               #그리고 R[0]는 제거해주고 앞으로 한칸씩 당겨줍니다.
        elif len(L) > 0:                #만약 L list에 값만 남았다면
            result.append(L[0])         #L list 자체는 sort가 되있으므로 
            L = L[1:]                   #결과값에 순서대로 넣어줍니다.   
        elif len(R) > 0:                #만약 R list에 값만 남았다면
            result.append(R[0])         #R list 자체는 sort가 되있으므로
            R = R[1:]                   #결과값에 순서대로 넣어줍니다.
    return result                       #최종 결과값을 minmax 함수로 이동시켜줍니다.


a = [4,5,2,3,6,8,1,7,9,90]
print(mergesort(a))

```

