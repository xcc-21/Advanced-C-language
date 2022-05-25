@[toc]
# 计算长度

## sizeof:

> 计算变量，数组，类型的大小，单位是字节（操作符）

```c
#include<stdio.h>
int main()
{
	//sizeof(数组名)-数组名表示整个数组的-计算的是整个数组的大小
	//&数组名 - 数组名表示的是整个数组，取出的是整个数组的地址
	//除此之外，所有的数组名都是数组首元素的地址

	//整形数组
	int a[]={1,2,3,4};
	printf("%d\n",sizeof(a));//16
	printf("%d\n",sizeof(a+0));//4/8 a+0是第一个元素的地址，sizeof(a+0)计算的是地址的大小
	printf("%d\n",sizeof(*a));//4 *a是数组的第一个元素，sizoef(*a)计算的是第一个元素的大小
	printf("%d\n",sizeof(a+1));//4/8  a+1是第二个元素的地址，sizeof(a+1)计算的地址的大小
	printf("%d\n",sizeof(a[1]));//4 计算的是第二个元素的大小

	printf("%d\n",sizeof(&a));// 4/8 -@a虽然数组的地址，但也是地址，sizeof(&a)计算的是一个地址的大小
	printf("%d\n",sizeof(*&a));//16 -计算的数组的大小
	//&a -- int(*p)[4]=&a;
	printf("%d\n",sizeof(&a+1));//4/8 - &a+1--数组后面的空间的地址
	printf("%d\n",sizeof(&a[0]));//4/8
	printf("%d\n",sizeof(&a[0]+1));//4/8

	//字符数组
	char arr[]={'a','b','c','d','e','f'};
	printf("%d\n",sizeof(arr));//6
	printf("%d\n",sizeof(arr+0));//4/8 -指针大小 -指针所指地址是4个字节地址
	printf("%d\n",sizeof(*arr));//1
	printf("%d\n",sizeof(arr[1]));//1
	printf("%d\n",sizeof(&arr));//4/8
	printf("%d\n",sizeof(&arr +1));//4/8
	printf("%d\n",sizeof(&arr[0]+1));//4/8
	return 0;
}

```

![请添加图片描述](https://img-blog.csdnimg.cn/4e21e19165ff4c65a28fcb43f3775049.png)
![请添加图片描述](https://img-blog.csdnimg.cn/ff95e968e7f740f985a04b0dcad71510.png)


```c
#include<stdio.h>
int main()
{
	//sizeof(数组名)-数组名表示整个数组的-计算的是整个数组的大小
	//&数组名 - 数组名表示的是整个数组，取出的是整个数组的地址
	//除此之外，所有的数组名都是数组首元素的地址

	//整形数组
	int a[]={1,2,3,4};
	printf("%d\n",sizeof(a));//16
	printf("%d\n",sizeof(a+0));//4/8 a+0是第一个元素的地址，sizeof(a+0)计算的是地址的大小
	printf("%d\n",sizeof(*a));//4 *a是数组的第一个元素，sizoef(*a)计算的是第一个元素的大小
	printf("%d\n",sizeof(a+1));//4/8  a+1是第二个元素的地址，sizeof(a+1)计算的地址的大小
	printf("%d\n",sizeof(a[1]));//4 计算的是第二个元素的大小


	printf("%d\n",sizeof(&a));// 4/8 -@a虽然数组的地址，但也是地址，sizeof(&a)计算的是一个地址的大小
	printf("%d\n",sizeof(*&a));//16 -计算的数组的大小
	//&a -- int(*p)[4]=&a;
	printf("%d\n",sizeof(&a+1));//4/8 - &a+1--数组后面的空间的地址
	printf("%d\n",sizeof(&a[0]));//4/8
	printf("%d\n",sizeof(&a[0]+1));//4/8


	//字符数组

	char arr[]={'a','b','c','d','e','f'};
	printf("%d\n",sizeof(arr));//6
	printf("%d\n",sizeof(arr+0));//4/8 -指针大小 -指针所指地址是4个字节地址
	printf("%d\n",sizeof(*arr));//1
	printf("%d\n",sizeof(arr[1]));//1
	printf("%d\n",sizeof(&arr));//4/8
	printf("%d\n",sizeof(&arr +1));//4/8
	printf("%d\n",sizeof(&arr[0]+1));//4/8

	return 0;
}
```

![请添加图片描述](https://img-blog.csdnimg.cn/bcb957342d5e45ea9a64d320917051a2.png)
![请添加图片描述](https://img-blog.csdnimg.cn/37c407ceacd6453593a304cd993b7dae.png)

```c

int main()
{
	int a[3][4] = { 0 };

	printf("%d\n", sizeof(a));//48 = 3*4*sizeof(int)
	printf("%d\n", sizeof(a[0][0]));//4 - a[0][0] - 是第一行第一个元素
	printf("%d\n", sizeof(a[0]));//16
	printf("%d\n", sizeof(a[0] + 1));//4 解释：a[0]作为数组名并没有单独放在sizeof内部，
									//也没取地址,所以a[0]就是第一行第一个算的地址
									//a[0]+1,就是第一行第二个元素的地址
	printf("%d\n", sizeof(*(a[0] + 1)));//4 - 解释：*(a[0] + 1)是第一行第二个元素

	printf("%d\n", sizeof(a + 1));//4 - 解释：a是二维数组的数组名，并没有取地址
	//也没有单独放在sizeof内部,所以a就表示二维数组首元素的地址，即：第一行的地址
	//a + 1就是二维数组第二行的地址

	printf("%d\n", sizeof(*(a + 1)));//16 解释：a+1是第二行的地址，所以*（a+1）表示第二行
	//所以计算的就是第2行的大小

	printf("%d\n", sizeof(&a[0] + 1));//4 解释：a[0]是第一行的数组名，
	//&a[0]取出的就是第一行的地址,&a[0]+1 就是第二行的地址

	printf("%d\n", sizeof(*(&a[0] + 1)));//&a[0]+1 就是第二行的地址
	//*(&a[0]+1) 就是第二行，所以计算的第二行的地址

	printf("%d\n", sizeof(*a));//16 解释：a作为二维数组的数组名，没有&，没有单独放在sizeof内部
	//a就是首元素的地址，即第一行的地址，所以*a就是第一行，计算的是第一行的大小

	printf("%d\n", sizeof(a[3]));//16 解释：a[3]其实是第四行的数组名（如果有的话）
	//所以其实不存在，也能通过类型计算大小的
	printf("%d\n", sizeof(a[-1]));

	return 0;
}
```



## strlen

> strlen:是求字符串长度的，只能对字符串长度（库函数-使用得引用头文件）

```c
#include<stdio.h>
#include<string.h>
int main()
{
	char arr[]={'a','b','c','d','e','f'};

	printf("%d\n",strlen(arr));//随机值  -遇到‘\0’结束
	printf("%d\n",strlen(arr+0));//随机值
	//printf("%d\n",strlen(*arr));//err
	//printf("%d\n",strlen(arr[1]));//err
	printf("%d\n",strlen(&arr));//随机值
	printf("%d\n",strlen(&arr+1));//随机值- 6
	printf("%d\n",strlen(&arr[0]+1));//随机值- 1

	return 0;
}
```

> 因为strlen只对字符串求长度，对字符会产生随机值

# 指针

### 指针变量的大小

32位计算机系统 整形指针占4个字节，实参传字符形参也是4个字节

> void test1 (char ch)//char *ch
> {
>
> ```c
>  printf("%d\n",sizeof(ch));//4个字节，因为传入的是字符的首地址，也就是指针char *ch ,指针长度为4，所以char字符类型的传参是传的指针字节
> ```
>
> }
> char arr[10]={0};
> printf("%d\n",sizeof(char));//10
> test1(ch);//字符数组首元素

- [ ] 只要在32位操作环境下，不管是什么类型，都是4个字节

![请添加图片描述](https://img-blog.csdnimg.cn/801c032f8f8340a7bb1069f5d54dc31d.png)




- [ ] 在64位环境下

![请添加图片描述](https://img-blog.csdnimg.cn/78dad213281c426c88bbd9b2026bb1a1.png)



### 声明指针

int* a,b,c;
事实上只声明了变量a是指针类型
如果要声明三个指针：
int *a ,*b, *c;



![请添加图片描述](https://img-blog.csdnimg.cn/5cc3bcb452d74d5b939854fd22528ade.png)


# 结构体

1. ​	. ：结构体变量.成员

2. ​    -> ：结构体指针->成员

   ![请添加图片描述](https://img-blog.csdnimg.cn/27095647d5a94e49b3aa37347737681c.png)


```c
#include<stdio.h>
#include<string.h>

struct Book
{
	char book_name[20];
	int price;
};

int main()
{
	struct Book b={"c语言程序设计",55};
	struct Book* p = &b;
	//更改价格
	(*p).price=19;//等同于p->price
	printf("%d\n",b.price);

	//更改书名
	//使用库函数字符串拷贝函数
	//b1.name="c++";//error
	strcpy(p->book_name,"C++");//因为book_name是字符型的数组名，数组本身是个地址，而price是变量
	printf("%s\n",(*p).book_name);

	printf("%s\t %d\n",p->book_name,p->price);
	printf("%s\t%d\n",(*p).book_name,(*p).price);//(*p).book_name,(*p).price等同于p->book_name,p->price
	printf("%s\n",b.book_name);
	printf("%d\n",b.price);

	return 0;
}
```

### 数组元素地址

> 1.sizeof(数组名),计算整个数组的大小，sizeof内部单独放一个数组名，数组名表示整个数组
> 2.&数组名，取出的数组的地址。&数组名，数组名表示整个数组。

除此1，2两种情况之外，所以的数组名都表示数首元素的地址

![请添加图片描述](https://img-blog.csdnimg.cn/23389c79574846db97cf71a6fe37521a.png)




# 字符串

### 字符串的比较

> stract(str1,str1); //err,因为自己追加自己会把'\0'覆盖掉，导致没有一直都没有'\0'反复循环

![请添加图片描述](https://img-blog.csdnimg.cn/d187056acad54f04ac7cad8b104e79c0.png)


不能用两个字符串比较两个字符串相等，应该使用字符串
例：

```c
char password[20]={0};
sacnf("%s",password);
//if(pwssword == "123456")//err
if(strcmp(password,"123456")==0)
printf("相同")；
```

### 字符串的拷贝

把字符串拷贝到目标地址，调试我们发现，遇到'\0'结束拷贝

```c
//更改书名
	//使用库函数字符串拷贝函数
	//b1.name="c++";//error
	strcpy(p->book_name,"C++");//因为book_name是字符型的数组名，数组本身是个地址
```

![请添加图片描述](https://img-blog.csdnimg.cn/df8b3017510d4516933cbe43a7f36e1a.png)


当拷贝的不是'\0'结束，程序运行出错

![请添加图片描述](https://img-blog.csdnimg.cn/402c5584f38241799c43660ca0dcb2f2.png)




- 源字符串必须以 '\0' 结束。
- 会将源字符串中的 '\0' 拷贝到目标空间。
- 目标空间必须足够大，以确保能存放源字符串。
- 目标空间必须可变。
- 学会模拟实现。
  **注意：源字符必须是字符数组或者是一个指向动态分配内存的数组的指针，不能使用字符串常量！**

# 结构体

### 内存对齐

总体来说：

> 结构体的内存对齐是拿空间来换取时间的做法。
> 起。

> S1和S2类型的成员一模一样，但是S1和S2所占空间的大小有了一些区别。

```c
//例如：
struct S1
{
char c1;
int i;
char c2;
};
struct S2
{
char c1;
char c2;
int i;
};
```

### 修改默认对齐数

之前我们见过了 #pragma 这个预处理指令，这里我们再次使用，可以改变我们的默认对齐数。

```c
//例如：
struct S1
{
 char c1;
 int i;
 char c2;
};
struct S2
{
 char c1;
 char c2;
 int i;
};
#include <stdio.h>
#pragma pack(8)//设置默认对齐数为8
struct S1
{
 char c1;
 int i;
 char c2;
};

#pragma pack()//取消设置的默认对齐数，还原为默认
#pragma pack(1)//设置默认对齐数为1
struct S2
{
 char c1;
 int i;
 char c2;
};
#pragma pack()//取消设置的默认对齐数，还原为默认
int main()
{
    //输出的结果是什么？
    printf("%d\n", sizeof(struct S1));
    printf("%d\n", sizeof(struct S2));
```




