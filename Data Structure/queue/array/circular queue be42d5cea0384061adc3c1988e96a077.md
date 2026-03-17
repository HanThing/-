# circular queue

: array페이지에서 작성한 queue배열과 약간의 차이가 있다. array페이지에서 작성한 queue는 하나의 요소당 한번만 입력 출력이 가능하다. circular queue는 이 부분을 보완하였다. 배열의 마지막 인덱스보다 1이 커지면, 0번 인덱스를 가르키도록 코드를 수정하였다. 

circular queue의 장점은 배열의 공간을 효율적으로 사용할 수 있다는 점이다. enqueue와 dequeue 연산이 배열의 양 끝에서 이루어지기 때문에, 배열이 가득 차기 전까지는 공간의 낭비가 발생하지 않는다.

배열의 크기가 5일 때, 실제로 사용하는 인덱스는 4개이다. 이는 rear(추가하는 인덱스)와 front(제거하는 인덱스)가 0부터 시작하기 때문이다. 즉, 배열의 첫 번째 요소는 비워두고, 두 번째 요소부터 데이터를 저장한다. 이렇게 하면, 배열의 끝에 도달했을 때 다시 처음으로 돌아가서 데이터를 저장할 수 있다.

create: queue배열을 생성하는 함수이다. rear과 front는 0으로 초기화한다.

enqueue: rear에 1을 더하는 대신, 1을 더한 후, 배열의 크기로 나눈 나머지를 구했다. 이 방식이 마지막 인덱스보다 1이커졌을때, 0이 되도록 해준다.

dequeue: 가장 처음에 입력된 값을 출력해준다.

display: for문을 사용하지 않은 이유는 배열이 가득 차있을 때, 반복문을 끝내는 조건이 반복문을 시작할때 상태와 같아서 반복문을 시작할 수 없어서 do~while문을 사용하였다.

```c
#include<stdio.h>
#include<stdlib.h>

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
    Q->front = Q->rear = 0;
    Q->q = (int *)malloc(sizeof(int *)*Size);
}

void enqueue(struct queue *Q, int x)
{
    if((Q->rear+1)%Q->size == Q->front)
        printf("queue is full\n");
    else
    {
        Q->rear=(Q->rear+1)%Q->size;
        Q->q[Q->rear] = x;
    }
}

int dequeue(struct queue *Q)
{
    int x=-1;
    
    if(Q->front == Q->rear)
        printf("queue is empty\n");
    else
    {
        Q->front = (Q->front+1)%Q->size;
        x = Q->q[Q->front];
    }
    return x;
}

void display(struct queue *Q)
{
    int i=(Q->front+1)%Q->size;
    do
    {
        printf("%d ", Q->q[i]);
        i=(i+1)%Q->size;
    }while(i!=(Q->rear+1)%Q->size);
    printf("\n");
}

int main(void)
{
    struct queue q;
    create(&q, 5);
    enqueue(&q, 1);
    enqueue(&q, 2);
    enqueue(&q, 3);
    enqueue(&q, 4); // rear가 가리키는 인덱스는 접근하지 않을거라서 q가 가득 찬 상태이다.
    enqueue(&q, 5); // 5는 안들어가진다.
    printf("%d\n", dequeue(&q));
    display(&q);

    return 0;
}
```