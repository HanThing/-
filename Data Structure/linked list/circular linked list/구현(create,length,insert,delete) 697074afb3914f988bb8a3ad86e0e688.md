# 구현(create,length,insert,delete)

```c
#include <stdio.h>
#include <stdlib.h>

struct NODE{
    int data;
    struct NODE *next;
}*head = NULL;

void create(int A[], int n)
{
    struct NODE *t, *last;
    head = (struct NODE *)malloc(sizeof(struct NODE));
    head->data = A[0];
    head->next = head;
    last = head;
    
    for(int i=1;i<n;i++)
    {
        t = (struct NODE *)malloc(sizeof(struct NODE));
        t->data = A[i];
        t->next = last->next;
        last->next = t;
        last = t;
    }
}

void display(struct NODE *p)
{
    do
    {
        printf("%d ", p->data);
        p = p->next;
    }while(p!=head);
}

void Rdisplay(struct NODE *p)
{
    static int flag=0;
    if(p!=head || flag==0)
    {
        flag=1;
        printf("%d ", p->data);
        Rdisplay(p->next);
    }
    flag=0;
}

int Length(struct NODE *p)
{
    int count=0;
    do
    {
        count++;
        p=p->next;
    }while(p!=head);
    
    return count;
}

void insert(struct NODE *p, int index, int Data)
{
    struct NODE *t;
    if(index<0 ||index>Length(p))
        return;
    if(index==0)
    {
        t = (struct NODE *)malloc(sizeof(struct NODE));
        t->data = Data;
        if(head==NULL)
        {
            head=t;
            head->next = head;
        }
        else
        {
            while(p->next!=head)
                p=p->next;
            t->next=head;
            p->next=t;
            head=t;
        }
    }
    else
    {
        t = (struct NODE *)malloc(sizeof(struct NODE));
        t->data = Data;
        for(int i=0 ; i<index-1 ; i++)
            p = p->next;
        t->next = p->next;
        p->next = t;
    }
}

int delete(struct NODE *p, int index)
{
    struct NODE *q=NULL;
    int x;
    if(index<=0 || index>Length(p))
        return -1;
        
    if(index==1)
    {
        while(p->next!=head)
            p=p->next;
        if(head==p)
        {
            x = head->data;
            free(head);
            head=NULL;
        }
        else
        {
            p->next=head->next;
            x = head->data;
            free(head);
            head=p->next;
        }
 
    }
    else
    {
        for(int i=0 ; i<index ; i++)
        {
            q=p;
            p=p->next;
        }
        q->next = p->next;
        x = p->data;
        free(p);
        
    }
    return x;
}

int main()
{
    int A[] = {1,2,3,4,5};
    create(A, 5);
    Rdisplay(head);
    printf("\n%d\n", Length(head));
    
    insert(head, 5, 6);
    display(head);
    printf("\n%d\n", delete(head, 1));
    display(head);

    return 0;
}
```