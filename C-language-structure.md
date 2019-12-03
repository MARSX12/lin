# lin
# C语言学习笔记--结构体

 - 
标签（空格分隔）： C学习笔记

---
##为什么使用结构？
思考: 如何存储一个班级中5名学员的信息(学号, 姓名, 性别和成绩)? 

 01  | 02 | 03 | 04 | 05 
|-----|----|----|----|----|    
 钱一|赵二|张三|李四|王五
|男   |女|男|女|男|
|60|70|80|90|100|
> 使用一维数组：不能确定数组间的关系

> 使用多维数组：C 语言不允许一个数组 包含多种数据类型
  
**因此需要使用结构体**

##什么是结构体

“结构” 是一种***构造数据类型***，它是由若干数据项组合而成的***复杂数据对象***，这些数据项称为结构的成员。

结构体定义的一般形式 
---
```
struct 结构体类型名 
{ 
    数据类型名1   成员名1；
    数据类型名2   成员名2； 
    … … 
    数据类型名n   成员名n； }；

```
```
struct Student 
{ 
    char num[10]; 
    char name[20]; 
    char sex; 
    int score; }；
```

结构体的嵌套定义 
---
结构体的成员可以又是一个结构体变量
```
struct Student 
{ 
    char num[10]; 
    char name[20]; 
    char sex; 
    struct Date birthday; 
    int sco
}
Date结构体如下
struct Date 
{ 
    int year; 
    int month; 
    int day;
}；
```

结构体的特点: 
---

 1. 结构体是一种构造类型, 它由若干”成员”组成.
 2. 每个成员可以是一个基本数据类型或者又是一个构造类型.
 3. 结构体不能包含自己的实例(即结构体变量)
 4. 结构体以包含指向自己实例的指针
    ```
    struct node 
    { 
        struct node next;   //Error 
    }；

    ```
    ```
    struct node 
    { 
        struct node *next;   //ok 
    }；

    ```
 5. 定义结构体并不分配内存空间 
        创建结构体的实例(变量)才会分配内存空间   

定义结构体变量
---

###1. 间接定义法： 先定义结构类型，再定义结构变量
```
struct 结构体类型名 
{ 
    数据类型名1   成员名1；
    数据类型名2   成员名2； 
    … … 
    数据类型名n   成员名n； }；
//struct 结构体类型名 变量名列表;
```
```
struct Student 
{ 
    char num[10]; 
    char name[20]; 
    char sex; 
    int score; }；
//struct Student  s1, s2, *p;    
```

###2. 直接定义法： 定义结构体类型的同时定义结构体变量
```
struct [结构体类型名] 
{ 
    数据类型名1   成员名1； 
    数据类型名2   成员名2； 
    … … 
    数据类型名n   成员名n； } 
\\变量名列表;
```

###3. 间接定义法：typedef 简化数据类型的书写
```
typedef struct [结构体类型名] 
{ 
    数据类型名1   成员名1； 
    数据类型名2   成员名2； 
    … … 
    数据类型名n   成员名n； 
} 结构体类型别名;
结构体类型别名 结构体变量名列表;
```
```
typedef struct [Stu] 
{ 
    char num[10]; 
    char name[20]; 
    char sex; 
    int score; 
} Student;
Student s1, s2, *p; 
struct Stu  s3, s4, *p2;
```

结构体变量的几点说明: 
---
1. 声明一个结构体的变量，将会为该变量分配内 存，大小是大于或等于其所有成员变量的大小之和。 
2. 只能对结构体类型变量赋值，存取，运算等。 而不能对结构体类型赋值，存取，运算等； 
3. 结构体中的成员如同普通变量一样，可以单独使用 
4. 结构体类型中的成员名可以与普通变量名相同. 但二者是彼此独立的,互不干扰

结构体变量的引用
---
引用方式: 成员运算符：结构体变量.成员 
说明：（注：先定义后使用）
1. 只能对结构体变量成员分别进行操作. 不能对结构体变量整体操作(取地址, 相互赋值除外) 
2. 同类型的结构体变量可以相互赋值: 值拷贝 
3. 有嵌套定义的结构体变量, 只能对低级别的结构体变量的成员操作
4. 对结构体变量中的成员操作与普通变量相同 
5. 允许使用成员和结构体变量的地址

结构体变量的初始化
---
方法1: 对成员逐个赋值 
方法2: 在定义变量时采用集合的方式, 对成员完全赋值 
```
//方法2
struct Student 
{ 
    char num[10]; 
    char name[20]; 
    char sex; 
    int score; 
} stu={"001","yan",'F',98}; 
struct Student s2={"001","yan",'F',98};
```

结构体数组的定义 
---
与结构体变量的定义方法相似

结构体数组的初始化
---
|num| name| sex |age| addr|
|-----|-----|----|----|----|
|10101| Diu Diu |M| 18| 721, SL Chengdu
|10102 |Dong Dong |F| 19 |9527, Shanghai
|10103| Xi Xi |F |18| 726, SL Beijing

方法1: 对成员逐个赋值 
方法2: 在定义变量时采用集合的方式, 对成员完全赋值 
```
struct [student] 
{  
    int num; char  name[20]; 
    char  sex; 
    int age; 
    char  addr[30]; 
} stu[3]={ {"10101", "Diu Diu", 'M', 18, "721, SL Chengdu"}, 
           {"10102", "Dong Dong", 'F', 19, "9527, Shanghai"}, 
           {"10103", "Xi Xi", 'F', 18, "726, SL Beijing"} };
```
注：小类型按最大类型增量分配空间

指向结构体变量的指针
---
注意:
1. 程序中*p表示 p 指向的结构体变量。 (*p).num 表示p指向的结构体变量中的成员num
2. (*p).num 等效于 p->num ->表示指向结构体成员运算符。
3. 结构体变量中成员的引用有三种形式:
    ① 结构体变量.成员名;
    ② (*p).成员名; 
    ③ p->成员名;
eg:
```
若有以下说明和语句： 
struct student 
{ 
    int age; 
    int num; 
}std,  *p; 
p=&std; 
则以下对结构变量std中成员age的引用方式正确的是(ABC) 
A) std.age    B) p->age    C) (*p).age     D) *p.age 
```
指向结构体的指针作函数参数
---
结构体变量的传递有三种形式: 
1. 用结构体变量的成员作参数。如: stu[1].num 
2. 用指向结构体变量(或数组)的指针作参数。 
3. 用整个结构体变量作参数。 (占用内存多,传递数 据速度慢)。
*注：结构体变量作为函数参数拷贝时是**值拷贝***
```
例：
typedef struct 
{    
    char name[9]; 
    char sex; 
    float score[2];  
}STU; 
void f(STU a) 
{ 
    STU b={"Zhao",'m',85.0,90.0};  
    int i; 
    strcpy(a.name,b.name); 
    a.sex=b.sex; 
    for(i=0;i<2;i++) 
    a.score[i]=b.score[i]; } 
main( ) 
{ 
    STU c={"Qian",'f',95.0,92.0}; 
    f(c) ; 
    printf("%s,%c,%2.0f,%2.0f\n",c.name,c.sex,c.score[0],c.score[1]); 
} 
程序的运行结果是( A )。 
A) Qian,f,95,92             B) Qian,m,85,90 
C) Zhao,f,95,92             D) Zhao,m, 85,90 
```

链表
---

###定义：
采用链式存储结构的链表是用一组任意的存储单元来存放线性表的数据元素，这组存储单元既可以是连续的，也可以是不连续的,甚至可以是零散分布在内存中的任何位置上。

###创建链表
```
typedef struct student{
	int score;//数据域
	struct student *next;//指针域
} LinkList;
```
> 一般创建链表都用typedef struct，因为这样定义结构体变量时，我们就可以直接可以用LinkList  *a;定义结构体类型变量了

###修改链表节点值
```
void change(LinkList *list,int n) //n为第n个节点
{
	LinkList *t = list;
	int i = 0;
	while (i < n && t != NULL) {
		t = t->next;
		i++;
	}
	if (t != NULL) {
		puts("输入要修改的值");
		scanf("%d", &t->score);
	}
	else {
		puts("节点不存在");
	}
}
```

###删除链表节点
删除链表的元素也就是把前节点的指针域越过要删除的节点指向下下个节点。即：p->next = q->next;然后放出q节点的空间，即free(q)
注：删除结点后结点储存空间还在，因此要用free()函数
```

void delet(LinkList *list, int n) {
	LinkList *t = list, *in;
	int i = 0;
	while (i < n && t != NULL) {
		in = t;
		t = t->next;
		i++;
	}
	if (t != NULL) {
		in->next = t->next;
		free(t);
	}
	else {
		puts("节点不存在");
	}
}
```

###插入链表节点
插入节点就是用插入前节点的指针域链接上插入节点的数据域，再把插入节点的指针域链接上插入后节点的数据域。根据图，插入节点也就是：e->next = head->next;  head->next = e;
```
void insert(LinkList *list, int n) {
	LinkList *t = list, *in;
	int i = 0;
	while (i < n && t != NULL) {
		t = t->next;
		i++;
	}
	if (t != NULL) {
		in = (LinkList*)malloc(sizeof(LinkList));
		puts("输入要插入的值");
		scanf("%d", &in->score);
		in->next = t->next;//填充in节点的指针域，也就是说把in的指针域指向t的下一个节点
		t->next = in;//填充t节点的指针域，把t的指针域重新指向in
	}
	else {
		puts("节点不存在");
	}
}
```
###输出链表
边遍历边输出
```
while (h->next != NULL) {
		h = h->next;
		printf("%d  ", h->score);
}
```
