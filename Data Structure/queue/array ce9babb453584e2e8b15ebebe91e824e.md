# array

: 배열에 queue의 형태로 데이터를 저장하였다. rear과 front는 배열의 인덱스를 나타내고, rear을 이용해 배열에 값을 넣어주고, front를 이용하여, 값에 접근하는 것을 막았다. 배열에 값은 들어있으나, 접근할 수 없는 구조이다. 따라서 배열의 각 요소는 한번씩만 enqueue하고, dequeue 할 수 있다.

create함수: queue배열을 생성하는 함수이다.

enqueue함수: 배열에 값을 넣어주는 함수이다.

dequeue함수: 가장 처음에 입력된 값을 출력해준다. 한번 출력하면, 그 요소에는 접근할 수 없다.

display함수: queue배열에 남아있는 값을 먼저 입력된 순서대로 출력해주는 함수이다.

```c
#include <stdio.h>
#include <stdlib.h>

struct queue
{
    int size;
    int front;
    int rear;
    int *q;
};

void create(struct queue *Q, int Size)
{
    Q->size = Size;
    Q->front = Q->rear = -1;
    Q->q = (int *)malloc(sizeof(int)*Size);
}

void enqueue(struct queue *Q, int x)
{
    if(Q->rear == Q->size-1)
        printf("Queue is full\n");
    else
    {
        Q->rear++;
        Q->q[Q->rear] = x;
    }
}

int dequeue(struct queue *Q)
{
    int x=-1;
    if(Q->rear == Q->front == -1)
        printf("queue is empty\n");
    else
    {
        Q->front++;
        x = Q->q[Q->front];
    }
    return x;
}

void display(struct queue *Q)
{
    for(int i=Q->front+1 ; i<=Q->rear ; i++)
    {
        printf("%d ", Q->q[i]);
    }
    printf("\n");
}

int main()
{
    struct queue q;
    create(&q, 5);
    enqueue(&q, 1);
    enqueue(&q, 2);
    enqueue(&q, 3);
    enqueue(&q, 4);
    enqueue(&q, 5);
    enqueue(&q, 6);
    printf("%d\n", dequeue(&q));
    display(&q);

    return 0;
}
```

[circular queue](array/circular%20queue%20be42d5cea0384061adc3c1988e96a077.md)

[](array/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EC%9D%8C%20cc217055821c4b09806e2c2db896ad50.md)