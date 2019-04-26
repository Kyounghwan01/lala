---
layout: post
title: "[취준] 필기테스트 대비"
date: 2018-10-26
excerpt: "데이터베이스, 통신, 알고리즘 등"
tag:
- 취준
category: [ 취준생활 ]
feature: https://png93.github.io/assets/img/title/basic.jpg
comments: true
---


## 데이터베이스 관련

### 정규화 (Normalization)

**정규화란?**  
__"이상현상(Anomaly)"과 "함수적 종속"에 의한 문제를 해결하기 위해 여러개의 릴레이션으로 분해하는 과정__  

[이상(Anomaly) 현상]  
- _참조 무결성, 개체 무결성_ 제약조건을 어기게 될 시 데이터의 중복과 종속으로 인해 발생하는 현상이다.
- 종류: 삭제, 삽입, 갱신 이상

  1. 삭제 이상 : 원하지 않는 자료까지 삭제가 되는 현상  
  2. 삽입 이상 : 원하지 않는 자료가 삽입되거나, 자료가 부족하여 삽입 되지 않는 현상 (개체무결성을 해친다.)  
  3. 갱신 이상 : 정확하지 않거나 일부 튜플만 갱신되는 현상

_개체 무결성: 기본키는 NULL이거나 중복값이 될 수 없다._  

[함수적 종속(Functional Dependency)]  
- 속성 A와 B에 대해, A의 값이 B값을 결정하는 경우 B는 A에 함수적으로 종속되었다고 한다.  

> 'A → B' : A = 결정자, B = 종속자  

- 종류: 완전 / 부분 / 이행적
  1. 완전 함수 종속 : '기본키'에만 종속되는 경우
  2. 부분 함수 종속 : 합성키의 일부 또는 기본키가 아닌 속성에 종속되는 경우
  3. 이행적 함수 종속 : 한다리 걸쳐서 종속되는 경우  
    A → B , B → C , A → C


[__정규화 (Normalization)__]  
- 종류: 1NF / 2NF / 3NF / BCNF / 4NF / 5NF (총 6단계)

1. 제 1 정규형 (1NF)  
테이블의 모든 도메인이 __원자값__ 만으로 구성 되도록 테이블을 분해한다.  

2. 제 2 정규형 (2NF)  
__부분함수종속을 제거__ 하기 위해 테이블을 분해한다.  

3. 제 3 정규형 (3NF)  
__이행함수종속을 제거__ 하기 위해 분해.  

4. BCNF (Boyce Codd Normal Form)  
__모든 결정자가 후보키가 되도록 분해하는 과정__  
==> 어떤 릴레이션에서 결정자가 후보키가 아닐 경우 수행한다.  

5. 제 4 정규형 (4NF)  
__다치종속 제거__  
_다치 종속 (MultiValued Dependency): 하나의 속성값이 속성의 집합을 결정하는 종속관계_  

6. 제 5 정규형 (5NF)  
__조인 종속__ 이 후보키를 통해서만 성립 되도록 한 정규형.  
_조인 종속: 원래의 릴레이션을 분해한 뒤 자연 조인한 결과가 원래의 릴레이션과 같은 결과가 나오는 종속성._  

cf) 역정규화 : 정규화를 진행하다가 테이블이 너무 많이 분해 되었을 경우, 검색을 수행하게 되면 분해된 만큼 조인 연산을 수행하므로 성능이 저하된다. 이러한 문제를 해결하기 위해 이상현상이나 종속이 일어나지 않는 부분까지 테이블을 다시 합치는 것을 '역정규화' 라고 한다.  

<br/>

#### 뷰(View)

정의: 테이블 또는 다른 뷰를 기초로 하는 논리적인 테이블.  
사용 목적:  
- 뷰를 사용하면 DB에서 선택적으로 데이터를 보여줄 수 있기 때문에 접근을 제한 할 수 있다.
- 복잡한 질의문으로 부터 결과를 검색하기 위한 단순한 질의를 만들 수 있다.  

#### 시퀀스(Sequence)

정의: 여러 사용자들이 공유하는 데이터베이스 객체. 호출 될 때마다 중복되지 않은 고유한 숫자를 리턴한다.  
_기본키 속성에 사용할 값을 발생시킬 때 사용한다._  

> 시퀀스명.NEXTVAL - 추출  
> 시퀀스명.CURRVAL - 참조

~~~sql
CREATE SEQUENCE emp_seq
INCREMENT BY 1
START WITH 100
MAXVALUE 9999
NOCACHE
NOCYCLE;
~~~


#### 인덱스(Index)
정의: 테이블에서 '행 = 튜플 = 레코드'를 검색할 때 검색 속도를 높이기 위해서 Oracle 서버가 사용하는 스키마 객체.  
- 인덱스를 사용하면 디스크의 I/O를 감소시킬 수 있다.
- 해당 테이블과 논리적으로 독립적이다.
- Oracle 서버에 의해 자동으로 관리된다.
- 테이블을 삭제하면 관련 인덱스는 자동으로 삭제된다.  

~~~sql
CREATE INDEX emp_ename_idx ON emp(ename);
~~~

<br/>

## 알고리즘 / 자료구조 관련

### 시간복잡도
- Big O : 알고리즘의 최악의 경우 성능을 의미
  - 최악의 경우 = __아무리 나빠도 이정도 성능을 보장__ 한다는 뜻이기 때문에 빅오 표현법을 가장 많이 사용한다.
- Big Omega : 최선의 경우
- Big Theta : 최악과 최선의 평균  

[빅오 표기법]  

> O(증가함수)


[자주 쓰이는 증가함수]  
_증가함수 : 데이터의 크기 n에 대해 알고리즘 수행시간이 증가하는 비율_  


 \\(O(1)\\) - 해시 테이블  
 \\(O(logN)\\) - __이진 탐색__  
 \\(O(N)\\)    - 순차 탐색  
 \\(O(NlogN)\\) - __퀵 정렬, 병합 정렬__  
 \\(O(N^{2})\\) - __거품 정렬, 삽입 정렬__  
 \\(O(N^{3})\\) - 행렬 곱셈  
 \\(O(2^{N})\\)  

<br/>

### 정렬 알고리즘

#### 1. 거품 정렬 (Bubble Sort) _ \\(O(N^{2})\\)

- 데이터 집합을 순회하면서 이웃 요소끼리 비교와 교환을 수행한다.
- 한번 순회가 끝날 때마다 가장 큰 값이 마지막에 위치하게 되며, 순회 할 범위가 1씩 줄어든다.  

거품 정렬의 비교횟수 = (n-1) + (n-2) + (n-3) + ... + 1 =
\\( \frac{n(n-1)}{2} \\)

~~~java
void bubbleSort(int[] data, int len) {

  for(int i = 0; i < len - 1 ; i++) {
    for ( int j = 0; j < len - (i+1); j++){
      if(data[j] > data[j+1]){
        int temp = data[j+1];
        data[j+1] = data[j];
        data[j] = temp;
      }
    }
  }

}
~~~

<br/>

#### 2. 삽입 정렬 _ \\( O(N^{2}) \\)  

- 데이터 집합을 순회 하면서 하나의 데이터와 그 앞 부분의 데이터들을 비교하여 들어갈 자리를 탐색 후 삽입하는 방법.  
- i번째 데이터를 정렬할 순서가 되었을 때, 0부터 i-1 까지의 데이터들은 정렬되어 있다.  

삽입 정렬 비교 횟수 = 1 + 2 + 3 + ... + (n-1) = \\( \frac{n(n-1)}{2} \\)  

~~~java
import java.util.Arrays;

void insertionSort(int[] data, int len){

  for(int i = 1; i < len; i++) {
    if(data[i-1] >= data[i]) continue;

    int value = data[i];
    for(int j = 0; j < i; j++) {
      if(data[j] > value){
        int[] temp = Arrays.copyOfRange(data, j, i);
        int ti = 0;
        for(int k = j + 1; k <= i; k++)
            data[k] = temp[ti++];
        data[j] = value;
        break;
      }
    }
  }

}
~~~
<br/>

#### 3. 퀵 정렬 _ \\( O(NlogN) \\)
1. 데이터 집합 내에서 기준 요소(Pivot) 하나를 선택한다.
2. 집합을 순회하면서 Pivot 보다 작은 값은 왼편에 큰 값은 오른편에 위치시킨다.
3. 더이상 나눌 수 없을 때 까지 왼쪽, 오른쪽으로 집합을 나누면서 1,2를 수행한다.  

~~~java
void quickSort(int[] data, int left, int right){

  if( left >= right) return;

  int pivot = (left + right) / 2;
  int first = left;
  int end = right;

  int temp = 0;

  while(left <= right) {
    while(data[left] <= data[pivot] && left < right)
      left++;

    while(data[right] > data[pivot] && left <= right)
      right--;

    if(left < right) {
      if(left == pivot) pivot = right;
      else if(right == pivot) = pivot = left;

      temp = data[left];
      data[left] = data[right];
      data[right] = temp;
    } else {
      break;
    }
  }

  temp = data[right];
  data[right] = data[pivot];
  data[pivot] = temp;

  quickSort(data, first, right-1);
  quickSort(data, right+1, end);

}
~~~
<br/>

#### 4. 병합 정렬 _ \\( O(NlogN) \\)
- 주어진 데이터 집합을 더 이상 나눌 수 없을 때 까지 나눈 후,
"정렬하면서" 병합하는 정렬 방법이다.  

~~~java
void mergeSort(int[] data, int start, int end){

  if(start >= end) return;

  int middle = (start + end) / 2;
  mergeSort(data, start, middle - 1);
  mergeSort(data, middle + 1, end);

  int left = start;
  int right = middle + 1;

  int[] mergeData = new int[end - start + 1];
  int mergeIndex = 0;

  // left 그룹과 right 그룹을 mergeData에 병합하며 정렬
  while(left <= middle && right <= end){
    if(data[left] < data[right]){
      mergeData[mergeIndex++] = data[left];
      left++;
    } else {
      mergeData[mergeIndex++] = data[right];
      right++;
    }
  }

  while(left <= middle)
    mergeData[mergeIndex++] = data[left++];

  while(right <= end)
    mergeData[mergeIndex++] = data[right++];

  mergeIndex = 0;
  for(int i = start; i <= end; i++){
    data[i] = mergeData[mergeIndex++];
  }

}
~~~
<br/>

### 자료구조

#### 스택(Stack)
- FILO 또는 LIFO 자료구조
- push(), pop()
- java.util.Stack
- 콜스택, 자동메모리 스택

#### 큐(Queue)
- FIFO 자료구조
- Enqueue: 삽입연산, 후단(Rear)에서 수행, offer()
- Dequeue: 제거연산, 전단(Front)에서 수행, poll()
- java.util.Queue 인터페이스  

#### 맵
- Key 와 Value 한쌍
- Key 값은 중복 허용하지 않음
- Key 값을 통해 Value 값 검색
- java.util.HashMap  

#### List
- 순서가 있고, 중복을 허용한다.
- ArrayList: 객체 내부 배열에 데잍를 저장
- LinkedList: 하나의 데이터를 갖는 노드 여러개를 연결


#### Set
- 순서가 없고, 중복을 허용하지 않는다.



## 네트워크

### OSI 7계층 모델

(7계층 → 1계층 순서)  
Application - Presentation - Session - Transport(TCP/UDP) - Network(IP) - DataLink - Physical  


### TCP/IP 모델
Application - Transport(TCP/IP) - Internet(IP) - DataLink - Physical


### TCP vs UDP
1. TCP (Trasfer Control Protocol)  
  - **신뢰성 높은** end-to-end 스트림 통신 프로토콜
  - **연결 지향**
  - 전송자가 보낸 순서대로 수신자에게 바이트가 도착
  - 데이터가 손실되는 상황을 막아주기 때문에 어플리케이션 코딩하기 쉬운 편

2. UDP (User Datagram Protocol)
  - **신뢰성 낮은** end-to-end 데이터그램 프로토콜
  - **비연결 지향**
  - 간단한 요청-응답 매커니즘에 기반하여, 패킷 손실 감지와 재전송은 상대편이 책임진다.  

_cf) TCP - 전화 / UDP - 편지_

TCP는 송수신 양단간 연결을 먼저 설정하고 양방향으로 데이터를 전송하며,  
UDP는 따로 연결 설정을 하지 않고 즉, 수신자가 데이터를 받을 준비를 했는지 확인하지 않고 단방향 전송을 수행한다.
{: .notice}

<br/>

## 운영체제

### 프로세스와 쓰레드  
 프로세스 = 공장, 쓰레드 = 일꾼으로 비유할 수 있다.  
 {: .notice}

[Process]
- 프로세스는 간단히 말해 '실행 중인 프로그램'이다.  
- OS로부터 메모리를 할당 받으면 프로세스가 된다.
- CPU가 할당되는 실체
- **운영체제가 관리하는 프로그램의 최소 단위**
- 실행(Run), 준비(Ready), 대기(Block) 상태가 있다.
- 프로세스는 데이터, 메모리, 쓰레드로 구성되어 있다.

[Thread]
- 하나의 프로세스에는 최소 하나 이상의 쓰레드가 존재한다.
- **프로세스의 자원을 이용하여 실제로 작업을 처리하는 실행의 흐름**
- 싱글쓰레드, 멀티쓰레드

<br/>

#### 멀티태스킹(멀티프로세싱)과 멀티쓰레딩
- 멀티태스킹: 여러 개의 프로세스가 동시에 실행되는 것
- 멀티쓰레딩: 하나의 프로세스 내에서 여러 쓰레드가 동시에 작업을 수행하는 것

<br/>

[멀티쓰레딩의 장점]
- 자원을 효율적으로 사용할 수 있다.
- 작업이 분리되어 코드가 간결해 진다.
- CPU 사용률을 향상시킨다.
- 채팅하면서 파일을 다운로드받고, 통화를 할 수 있는 이유가 멀티쓰레드로 작성되어 있기 때문이다.  

[멀티쓰레딩의 단점]
- 여러 쓰레드가 같은 프로세스 내에서 자원을 공유하면서 작업 하기 때문에 **Synchronization(동기화), DeadLock(교착상태)** 과 같은 문제들을 고려해야 한다.  

_교착상태: 두 쓰레드가 자원을 점유한 상태에서 서로 상대편이 점유한 자원을 기다리느라 진행이 멈춰있는 상태_  


---
