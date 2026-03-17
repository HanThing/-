# Parantheses Matching

<aside>
💡 :주어진 문자열에 포함된 소괄호()가 올바르게 열리고 닫혔는지 판단하는 함수(IsBalanced)를 구현하였다. 열린괄호’(’ 는 스택에 push한다. 닫힌괄호 ‘)’는 스택이 차있으면,  pop해준다. 그러나, 닫힌괄호’)’에 대해 판단할때, 스택이 비어있다면, 해당하는 문자열은 소괄호가 올바르지 못한 순서라고 판단한다.

</aside>

push함수 :주어진 문자열에 ‘(’가 있으면, 스택에 넣어준다.

pop함수 :주어진 문자열에 ‘)’가 있으면, 스택에서 ‘(’를 지워준다.

display함수 :스택에 들어있는 데이터를 출력해준다. parantheses Matching을 함에 있어서는 불필요한 함수이다.

IsBalanced함수 :전달받은 문자열의 소괄호가 매칭이 되는지 확인하는 함수이다.

```c
#include <stdio.h>
#include <stdlib.h>
struct Node
{
    int data;
    struct Node *next;
}* top=NULL;

void push(char x)
{
    struct Node *t = (struct Node *)malloc(sizeof(struct Node));
    
    if(t==NULL)
        printf("stackover flow\n");
    else
    {
        t->data=x;
        t->next=top;
        top=t;
    }
}

char pop()
{
    char x=-1;
    struct Node *t = (struct Node *)malloc(sizeof(struct Node));
    
    if(top==NULL)
        printf("stack is empty\n");
    else
    {
        t=top;
        top=t->next;
        x=t->data;
        free(t);
    }
    return x;
}

void display()
{
    struct Node *p;
    p=top;
    if(p==NULL)
        printf("stack is empty\n");
    else
    {
        while(p!=NULL)
        {
            printf("%d ", p->data);
            p=p->next;
        }
    }
    
}

int IsBalanced(char *Exp)
{
    for(int i=0;Exp[i]!='\0';i++)
    {
        if(Exp[i]=='(')
            push(Exp[i]);
        else if(Exp[i]==')')
        {
            if(top==NULL)
                return 0;
            pop();
        }
    }
    if(top==NULL)
        return 1;
    else
        return 0;
}

int main()
{
    char *exp={"((a+b)*(c-d))"};
    
    printf("%d\n", IsBalanced(exp));

    return 0;
}
```