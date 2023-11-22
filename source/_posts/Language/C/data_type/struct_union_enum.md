---
title: 结构联合枚举
tags:
  - C
categories:
  - Language
  - C
  - data_type
---
# 结构体（structure）

## 1. 设置结构样式、定义结构变量、访问结构体成员

- book 是 tag（标记）。
- 可以把一个结构体变量的值赋给另一个结构体变量

```c
struct book{			//设置结构体样式。有作用域。book是tag（标记）.
    char title[MAXTITL];  //结构成员列表
    char author[MAXAUTL];
    float value;
};
struct book library;   //声明结构体变量
printf("%s by %s: %.2f\n", library.title, library.author, library.value); //访问结构体成员
//. 是结构成员运算符，优先级比 & 高
```

## 2. 三种定义结构体变量的方式

```c
//1. 用关键字定义变量
struct book library;

//2. 设置结构体样式时定义变量（有样式名）
struct book{
    char title[MAXTITL];
    char author[MAXAUTL];
    float value;
}library;

//3. 没有样式名
struct{
    char title[MAXTITL];
    char author[MAXAUTL];
    float value;
}library;
```

## 3. 初始化结构体变量

```c
struct book{
    char title[MAXTITL];
    char author[MAXAUTL];
    float value;
};
struct book library = {
"The Pious Pirate and the Devious Damsel",
"Renee Vivotte",
1.95
};

typedef struct list
{
    node *head;
    node *tail;
}list;
list temp={NULL};//全部设为NULL了
```

## 4. 初始化结构体数组

```c
struct node
    {
        int data;
        int next;
    }pool[N]={0};//全部初始化为0

struct Student
{
  int num;
  char name[10];
  char sex;
};
struct Student students[3]={
{0001, "Zhang San",'M'},
{0002, "Li Si",'W'},
{0003, "Zhao Liu",'M'}
};
```

## 5. 嵌套结构

```c
struct names
{
    char first[LEN];
    char last[LEN];
};
struct guy
{
    struct names handle;
    char favfood[LEN];
    char job[LEN];
    float income;
};
```

## 6. 指针

```c
struct guy fellow[2], *him;
him=fellow;
him->income; 
//相当于 (*him).income
//连接号(-)后跟一个大于号(>)
//- 读作 hyphen /ˈhaɪfn/
//> 读作 greater than sign

S->top++;
S->data[S->top]=e;
//箭头运算符的优先级
```

## 7. 向函数传递结构的信息

以结构体变量（不是数组）为参数时，会在函数里创建副本。

## 8. 结构体的复合字面量（结构体常量）(C99)

```c
(struct book) {"Crime and Punishment",
"Fyodor Dostoyevsky",
11.25};
//复合字面量

&(struct book) {"Crime and Punishment",
"Fyodor Dostoyevsky",
11.25};
//复合字面量的地址
```

## 9. 伸缩型数组成员（C99）

结构体的最后一个成员是长度未定的数组。需要由 malloc 指定。

```c
struct flex
{
size_t count;
double average;
double scores[];
};
struct flex * pf1;
pf1 = malloc(sizeof(struct flex) + n * sizeof(double));
```

特殊的处理要求。第一，不能用结构进行赋值或拷贝：

```c
struct flex * pf1, *pf2;
// *pf1 和*pf2 都是结构
...
*pf2 = *pf1;
// 不要这样做
```

这样做只能拷贝除伸缩型数组成员以外的其他成员。确实要进行拷贝，应使用memcpy()函数。

第二，不要以按值方式把这种结构传递给结构。原因相同，按值传递一个参数与赋值类似。要把结构的地址传递给函数。

第三，不要使用带伸缩型数组成员的结构作为数组成员或另一个结构的成员。

## 10. 匿名结构 (C11)

```c
struct person
{
int id;
struct {char first[20]; char last[20];}; // 匿名结构
};//设置样式
struct person ted = {8483, {"Ted", "Grass"}};//初始化
puts(ted.first);//引用
```

## 11. 保存结构到文件

```c
fprintf();//可移植性好，但是太麻烦
fwrite();//可移植性不好，但是很简单
```

## 12. 指定初始化器

```c
//可以按照任意顺序使用指定初始化器：
struct book gift = {
.value = 25.99,
.author = "James Broadfool",
.title = "Rue for the Toad"};
```

# 联合（union）数据类型

union 能存储不同的数据类型；用成员运算符（.）访问，也可用间接成员运算符（->）用指针访问；有匿名联合。
hold 是 tag（标记）。

```c
union hold {
int digit;
double bigfl;
char letter;
};//声明样式，与structure格式相同

//声明变量
union hold valA;
valA.letter = 'R';
union hold valB = valA; // initialize one union to another
union hold valC = {88}; // initialize digit member of union
union hold valD = {.bigfl = 118.2}; // designated initializer

//访问成员
fit.digit = 23;
pu = &fit;
x = pu->digit;// same as x = fit.digit
```

匿名联合

```c
struct owner {
char socsecurity[12];
...
};
struct leasecompany {
char name[40];
char headquarters[40];
...
};
struct car_data {
char make[15];
int status; /* 0 = owned, 1 = leased */
	union {
	struct owner owncar;
	struct leasecompany leasecar;
	};
...
};
```

# 枚举（enumerated type）

```c
enum spectrum {red, orange, yellow, green, blue, violet};  //声明枚举样式，与structure格式相同
enum spectrum color;//声明变量

//运用枚举变量
int c;
color = blue;
if (color == yellow)
...;
for (color = red; color <= violet; color++)
...;
```

- 枚举变量的值是 int 类型。
- 默认情况，枚举列表中的常量都被赋予0、1、2等。因此，下面的声明中 nina 的值是3：enum kids {nippy, slats, skippy, nina, liz};
- 在枚举声明中，可以为枚举常量指定整数值：enum levels {low = 100, medium = 500, high = 2000};
- 如果只给一个枚举常量赋值，没有对后面的枚举常量赋值，那么后面的常量会被赋予后续的值。例如，假设有如下的声明：enum feline {cat, lynx = 10, puma, tiger};那么，cat的值是0（默认），lynx、puma和tiger的值分别是10、11、12。

# 共享名称空间（P410）

