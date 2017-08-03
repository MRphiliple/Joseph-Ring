## Joseph-Ring
###约瑟夫环问题
```c++
//猴子选大王
//约瑟夫环问题

#include<stdio.h>
#include<malloc.h>
#define LEN sizeof(struct monkey)

struct monkey
{
	int a;
	struct monkey* next;
};
struct monkey *creat(int);//创建猴子循环链表
int countmonkey(struct monkey*,int,int);//选出最后一个猴子

int main()
{
	int n,m,last;   //n-猴子总数   m-第m个猴子退出
	struct monkey *head;
	scanf("%d %d",&n,&m);
	head=creat(n);
	last=countmonkey(head,m,n);
	printf("最后一个猴子是第%d个 \n",last);
	return 0;
}

struct monkey *creat(int n)
{
	 int i=1;
	 struct monkey *head,*p1,*p2;
     p1=p2=(struct monkey*)malloc(LEN);
     p1->a=i;
     head=p1;
     do
     {  i++;
        p1=(struct monkey*)malloc(LEN);
        p1->a=i;p2->next=p1;p2=p1;
     }while(i<n);
     p2->next=head;
	 return(head);
}

int countmonkey(struct monkey *head,int m,int n)
{
	struct monkey *p1,*p2;
	p1=head;
	int i,j;
	for(i=1;i<n;i++)
	{
		for(j=1;j<m;j++)
        {
            p2=p1;
            p1=p1->next;
        }
		p1->a=0;                //通过删除节点来排除猴子
		p2->next=p1->next;
		p1=p1->next;
	}
	return p1->a;     //最后剩下的猴子为猴王，不在需要循环
}


```
