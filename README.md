#include<stdio.h>
char stack[100];
int top = -1;
int priority(char ele)
{
    if(ele == '(')
        return 0;
    if(ele == '+' || ele == '-')
        return 1;
    if(ele == '*' || ele == '/')
        return 2;
}
char pop()
{
    if(top == -1)
        return -1;
    else
        return stack[top--];
}
void push(char ele)
{
    stack[++top] = ele;
}

int main()
{
    char exp[100];
    char *ptr, ele;
    printf("Enter the expression :: ");
    scanf("%s",exp);
    ptr = exp;
    while(*ptr != '\0')
    {
        if(isalnum(*ptr))
            printf("%c",*ptr);
        else if(*ptr == '(')
            push(*ptr);
        else if(*ptr == ')')
        {
            while((ele = pop()) != '(')
                printf("%c",ele);
        }
        else
        {
            while(priority(stack[top]) >= priority(*ptr))
                printf("%c",pop());
            push(*ptr);
        }
        ptr++;
    }
    while(top != -1)
    {
        printf("%c",pop());
    }
}
