# linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct Node
{
    int data;
    struct Node *next;
}*front=NULL, *rear=NULL;

void enqueue(int x)
{
    struct Node *t;
    t=(struct Node *)malloc(sizeof(struct Node));
    

    
    if(t==NULL)  
        printf("queue is full\n");
    else
    {
        t->data = x;
        t->next = NULL;
        
        if(front==NULL)
        {
            front = rear = t;
        }
        else
        {
            rear->next = t;
            rear = t;
        }
    }
}

int dequeue()
{
    struct Node *t;
    int x=-1;
    if(front==NULL)
        printf("queue is empty\n");
    else
    {
        x= front->data;
        t=front;
        front = front->next;
        free(t);
    }
    return x;
}

void display()
{
    struct Node *p;
    p=front;
    while(p!=NULL)
    {
        printf("%d ", p->data);
        p = p->next;
    }
    printf("\n");
}

int main()
{
    enqueue(1);
    enqueue(2);
    enqueue(3);
    enqueue(4);
    enqueue(5);
    printf("%d\n", dequeue());
    display();
    
    return 0;
}

```