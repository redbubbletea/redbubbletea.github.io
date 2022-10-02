---
sort: 1
---

# 인접리스트

22.10.02

## 기초
   
자연수를 입력 받고, 인접리스트 방식으로 넣고 출력하고 빼기.   

~~~c
#include<stdio.h>
#include<stdlib.h>

typedef struct _node{ // 각 노드
  int data;
  struct _node * next;
} Node;

int main(void){
  Node * head = NULL;
  Node * tail = NULL;
  Node * cur = NULL;

  Node * newNode = NULL;
  int readData;

  // 데이터를 입력받는 과정 //
  while(1){
    printf("자연수 입력: ");
    scanf("%d", &readData);
    if(readData < 1) // 0 이하 입력 시 중단
      break;
    
    // 노드의 추가 과정
    newNode = (Node*)malloc(sizeof(Node)); //노드 동적 할당
    newNode->data = readData; // 입력 받은 데이터 넣기
    newNode->next = NULL; // 마지막 순서로 만들기

    if(head == NULL) // 첫 노드라면
      head = newNode;
    else
      tail->next = newNode;

    tail = newNode;
  }
  
  // 데이터 출력 //
  printf("입력 받은 데이터의 전체 출력! \n");
  if(head == NULL)
    printf("저장된 자연수가 존재하지 않습니다. \n");
  else{
    cur = head;
    printf("%d ", cur->data); // 첫번째 데이터 출력

    while(cur->next != NULL){ // 두번째 이후의 데이터 출력
      cur = cur->next;
      printf("%d ", cur->data);
    }
  }

  printf("\n\n");

  // 메모리 해제 //
  if(head == NULL)
    return 0;
  else{
    Node * delNode = head;
    Node * delNextNode = head->next;

    printf("%d을(를) 삭제합니다. \n", head->data);
    free(delNode); // 첫번째 노드 삭제
    
    while(delNextNode != NULL){ // 두번째 이후 노드 삭제
      delNode = delNextNode;
      delNextNode = delNextNode->next;

      printf("%d을(를) 삭제합니다. \n", delNode->data);
      free(delNode);
    }
  }

  return 0;
}
~~~


## 직접 만들기

헤더 파일을 만들고, 함수를 작성해서 인접리스트 코딩하기.

~~~c
#include <stdio.h>
#include <stdlib.h>
#include "DLinkedList.h"

int WhoIsPrecede(int d1, int d2){
  if(d1 < d2)
    return 0;
  else
    return 1;
}

int main(void) {
  List list;
  int data;
  ListInit(&list);
  SetSortRule(&list, WhoIsPrecede);

  LInsert(&list, 11);
  LInsert(&list, 11);
  LInsert(&list, 22);
  LInsert(&list, 22);
  LInsert(&list, 33);

  printf("current data num : %d\n", LCount(&list));

  if (LFirst(&list, &data)) {
    printf("current data : %d\n", data);

    while (LNext(&list, &data)) {
      printf("current data : %d\n", data);
    }
  }

  if (LFirst(&list, &data)) {
    if(data == 22) LRemove(&list);
    while (LNext(&list, &data)) {
      if(data == 22)
        LRemove(&list);
    }
  }

  printf("\n");

  if (LFirst(&list, &data)) {
    LRemove(&list);
    while (LNext(&list, &data)) {
      LRemove(&list);
    }
  }

  printf("current data num : %d\n", LCount(&list));
  return 0;
}
~~~

헤더 파일은 [이곳](https://replit.com/@yejiya7/LinkedList2#DLinkedList.h)에서.