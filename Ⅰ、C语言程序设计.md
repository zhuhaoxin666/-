## Ⅰ、C语言程序设计

###   一、C语言概述

#### 1.起源

+ 贝尔实验室
+ 作者: ken Thompson ，Dennis Ritchie

#### 2.标准化

+ ANSI / ISO

#### 3.优缺点

+ 性质：
  + C语言是一种低级语言
  + C语言是一种小型语言
  + C语言是一种包容性语言
+ 优点
  + 高效性
  + 可移植性
  + 功能强大
  + 灵活性
  + 标准库
  + 与UNIX系统的集成
+ 缺点
  + C程序可能会漏洞百出
  + C程序可能会难以理解
  + C程序可能会难以修改

#### 4.编译和链接

+ 预处理：首先会把程序送交给预处理器。预处理器执行以#开头的指令
+ 编译：修改后的程序进入编译器，编译器会把程序翻译成机器指令（目标代码）。
+ 链接：在最后一个步骤中，链接器把由编译器产生的目标代码和任何其他附加代码整合在一起，这样才最终产生了完全可执行的程序
+ 通常把C语言编译器命名为cc



#### 5.关键字

+ auto
+ const
+ do
+ enum
+ extern
+ register
+ signed
+ sizeof
+ struct
+ typedef
+ union
+ volatile



### 二、表达式

#### 1.算数运算符

+ 一元运算符：+ ，- ，表示正负，仅一个操作数。比如：int i = +1; int j = -1;

+ 二元运算符：
  + 加法类：
    + +加法运算符
    + -减法运算符
  + 乘法类
    + *乘法运算符
    + /除法运算符
    + %取余运算符 ：%运算符要求两个操作数都是整数，否则编译不通过
+ 优先级
  + 一元运算符 > 二元乘除 > 二元加减

#### 2.赋值运算符

+ 复合赋值运算：+= ，-=，*=，/=，%=
+ 自增减运算符：++i , i++
  + 前缀++ i 指先自增再运算
  + 后缀i ++ 指的是先运算再自增
+ 优先级：
  + 后缀自增 > 前缀自增 > 一元运算符 > 二元乘除 >二元加减

#### 3.关系运算符

+ 包含：> ，<，>= , <=  , 关系运算符优先级低于算数运算符

#### 4.判等运算符

+ 包含： == 、!=
+ 判等运算符的优先级低于关系运算符

#### 5.逻辑运算符

+ 包含：! , || , &&
+ 其中 ！为一元运算符。||，&&为二元运算符
+ || ，&& 优先级低于关系运算符和判等运算符

#### 6.三元运算符

+ 表达式1 ？ 表达式2 ： 表达式3

#### 7.逗号运算符

+ int a = （3，5）; 得到 a=5

### 三、数据类型

#### 1.整型

> 整数通常以16位或32位方式存储，在有符号数中，如果数为整数或零，那么最左边的符号位为0，如果是负数，符号位是1。

+ 有符号的 
  + 16位存储：最大的16位数为32767（即2^15-1）, 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
  + 32位存储：最大的32位数为2147483647（即2^31-1）
+ 无符号的
  + 16位存储：不保留符号位，2^16-1 = 65535
  + 32位存储：2^32-1

> > **默认情况都是有符号数**
>
> + 取值范围
>
>   + 16位机
>
>   + 注意：short int 和 int 有相同的取值范围
>
>     |        类型        | 最小值 | 最大值 |
>     | :----------------: | :----: | :----: |
>     |     short int      | -32768 | 32767  |
>     | unsigned short int |   0    | 65535  |
>     |        int         | -32678 | 32767  |
>     |    unsigned int    |   0    | 65535  |
>     |      long int      |        |        |
>     |   unsigned long    |        |        |
>
>   + 32位机
>
>   + int 和 long有相同的取值范围
>
>     |        类型        | 最小值 | 最大值 |
>     | :----------------: | :----: | :----: |
>     |     short int      | -32678 | 32767  |
>     | unsigned short int |   0    | 65535  |
>
>   
>
>   

#### 2.浮点型

+ 单精度：float   IEEE标准：6个数字
+ 双精度：double IEEE标准：15个数字
+ 扩展双精度：long double



#### 3.字符型

+ 注意，C语言字符常量用单引号。 char a = ' A ';
+ ASCII 码：'a' = 97 , 'A' = 65, '0' = 48, 大小写之间差32



###	三、数组

+ 定义方式：
  + int a[10]; int a[6] = {1,2,3,4,5,6}, int a[] = {1,2,3};
  
+ 多维数组
  + int a[5] [5];
  
+ **动态开辟数组**

  + ```c
    
    //使用malloc
    int main() {
    
        int n;
        scanf("%d",&n);
        int *a,*p;
        a = malloc(n*sizeof(int));
        p = a;
        for(;p<a+n;p++){
            scanf(" %d",p);
        }
    
        p = a;
        for(;p<a+n;p++){
            printf("%d ",*p);
        }
    
        return 0;
    }
    ```

    

  ```
  //使用calloc和malloc的区别
  //calloc会清除分配的内存的已有值，而malloc不会
  // calloc(n,sizeof(int)); malloc(n*sizeof(int));
  
  
  int main() {
  
      int n;
      scanf("%d", &n);
      int *a, *p;
  //    a = malloc(n * sizeof(int)); // 输出 -99064976 515 -99090096 515 1769096192
      a = calloc(n,sizeof(int)); //输出 0 0 0 0 0
      p = a;
  //    for(;p<a+n;p++){
  //        scanf(" %d",p);
  //    }
  
      p = a;
      for (; p < a + n; p++) {
          printf("%d ", *p);
      }
  
      return 0;
  }
  ```

+ realloc : 动态修改已分配内存块的大小

  + 注意：realloc作用于由malloc，calloc，realloc分配的内存块，对其他的内存块可能会有异常。

  + > void * realloc(void * ptr, size_t size );

  + 如果realloc函数不能按照要求扩大内存块将返回NULL

  + 如果第一个参数传NULL，那么realloc和malloc行为就一致了

  + 如果第二个参数传0，那么realloc和free行为就一致了

+ 释放内存

  + free 

  + > void free(void * ptr);

#### 四、函数：

+ 返回类型  函数名(参数){

  

  }

+ 注意：函数若定义在main函数之后，必须现在main函数之前声明。

  > ​	float average(float a,float b){
  >
  > ​		return (a+b)/2;
  >
  > ​    }
  >
  > ​    int main(){return 0;}
  >
  > 或者 
  >
  > ​	float average(float a,float b); //声明
  >
  > ​	int main(){return 0;}
  >
  > ​	float average(float a,float b){
  >
  > ​    	return (a+b)/2;
  >
  > ​	}	 

+ 函数不用指针的话普通类型是值传递，数组是地址传递



###	五、指针

+ 定义：指针就是地址，指针变量是只存储地址的变量

+ int *p , float *q, char *c

+ 指针可以指向另一个指针，即指向指针的指针

  > int *p ;
  >
  > int i;
  >
  > p = &i;
  >
  > 上述语句把p指向i的地址
  
+ 指针作为参数

  > int add(int *a,int *b){
  >
  > ​	 int res = *a + *b;
  >
  > ​	 return res;
  >
  > }
  >
  > //调用时
  >
  > int main(){
  >
  > ​    int a = 5;
  >
  > ​    int b = 4;
  >
  > ​    int ans  = add(&a,&b);
  >
  > }

  + 指针作为返回类型

    > ​	int* getMax(int *a,int *b){
    >
    > ​    	return *a > *b ? a : b;
    >
    > ​     }
    >
    > //调用时:
    >
    > int main(){
    >
    > ​	int a = 9;
    >
    > ​	int b= 8;
    >
    > ​	int *ans = getMax(&a,&b);
    >
    > }

+ 指针指向数组

  + 首先，本身数组就是指针。

  > int a[5] = {1,2,3,4,5};
  >
  > int *p = a 和 int *p = &a[0] 无区别；
  >
  > *a = 7 相当于 a[0] = 7; *(a+1) = a[1]

  + 指针用于数组处理

    > #define N 10
    >
    > int a[N],sum,*p;
    >
    > sum =0;
    >
    > //数组求和
    >
    > //第一种写法
    >
    > for(p = &a[0];p<&a[N];p++){
    >
    > ​     sum+=*p;
    >
    > }
    >
    > 
    >
    > //第二种写法
    >
    > for(p=a;p<a+N;p++){
    >
    > ​	sum+=*p;
    >
    > }
    >
    > 
    >
    > //第三种写法，指针作为数组名
    >
    > for(int i=0;i<N;i++){
    >
    > ​	sum+=p[i];
    >
    > }

+ 指针处理多维数组

  > int a[NUM_ROWS] [NUM_COLS];
  >
  > int row,col;
  >
  > int *p;
  >
  > //给a数组清除掉
  >
  > for(p = &a[0] [0] ;p<=a[NUM_ROWS-1] [NUM_COLS-1] ;p++){
  >
  > ​	*p = 0;
  >
  > }
  >
  > //处理二维数组中的指定列
  >
  > for(p = a[i] ; p < a[i] + NUM_COLS ;p++){
  >
  > ​	*p =0;
  >
  > }

  

### 六、文件

+ 源文件：.c文件
+ 头文件：.h文件
+ 在源文件中添加: include "my.h"使用
+ 头文件中也可使用include引用其他头文件
+ 为避免头文件的反复编译，应该使用#ifndef 和 #endif

**关于文件的IO**

+ 打开文件

  > FILE * fopen(const char *filename,const char *mode)
  >
  > fopen函数会返回一个文件指针，通常将此指针存入一个变量中。
  >
  > fp = fopen("in.dat","r");
  >
  > r表示只读。
  >
  > 关于模式（函数fopen的参数mode）：
  >
  > | 字符串 |                   含义                   |
  > | :----: | :--------------------------------------: |
  > |  "r"   |              打开文件用于读              |
  > |  "w"   |     打开文件用于写（文件不需要存在）     |
  > |  "a"   |    打开文件用于追加（文件不需要存在）    |
  > |  "r+"  |     打开文件用于读和写，从文件头开始     |
  > |  "w+"  | 打开文件用于读和写（如果文件存在就截去） |
  > |  "a+"  | 打开文件用于读和写（如果文件存在就追加） |
  >
  > 注意：当打开的文件是二进制文件，需要在字符串中包含b
  >
  > 如：rb，wb，r+b/rb+...

+ 关闭文件

> int fclose(FILE *stream);
>
> 如果成功关闭，该函数会返回0，否则返回错误代码EOF

+ 举例

  > //读
  >
  > ```c
  > FILE *fp;
  > fp = fopen("D:\\360sd\\untitled2\\test.txt","r");
  > if(fp == NULL){
  >     printf("FILE NOT FOUND");
  > }
  > 
  > char ch;
  > 
  > for(ch = fgetc(fp);ch != EOF ;){
  >     printf("%c",ch);
  >     ch = fgetc(fp);
  > }
  > fclose(fp);
  > ```
  >
  > //写
  >
  > ```c
  > FILE *fp;
  > fp = fopen("D:\\360sd\\untitled2\\write.txt","w");
  > if(fp == NULL){
  >     printf("FILE NOT FOUND");
  > }
  > 
  > char ch;
  > ch =getchar();
  > while(ch != '\n'){
  >     fputc(ch,fp);
  >     ch = getchar();
  > }
  > return 0;
  > ```

+ 删除文件

  > remove("文件名") , 成功返回0，否则返回非0值

+ 文件更名

  > rename("oldname","newName") 成功返回0，否则返回非0值



### 七、结构、联合、枚举

#### 1.结构(struct)

+ 定义：

  ```c
  struct{
      int number;
      char name[10];
      int age;
  }stu1,stu2;
  ```

  ```c
  
  //定义初始化
  struct{
      int number;
      char name[10];
      int age;
  }stu1 ={001,"peter",20},stu2={002,"lisa",22};
  ```

  ```c
  
  //给一个“student名字”，可以再通过student定义新的stu，比如 struct student stu3;
  struct student{
      int number;
      char name[10];
      int age;
  };
  
  
  ```

  ```c
  
  //使用typedef struct 定义的结构在之后调用声明结构时，不用加struct
  #include<stdio.h>
  #include<stdlib.h>
  #include<string.h>
  
  typedef struct{
      int number;
      char name[10];
      int age;
  }Student;
  
  
  int main(){
  
      Student stu;
      strcpy(stu.name,"zhuhaoxin");
      printf("%s",stu.name);
  
      return 0;
  }
  ```

#### 2.联合(union)

+ 定义：

  ```c
  union{
      int a;
      float b;
  }u;
  
  ```

+ 与结构的区别
  + 联合的地址空间是交叉的，会把空间分配给最大的成员，所以如果给上面的那个联合的a，b赋值，会导致a的数据丢失，b的数值也可能出现问题



### 八、位运算

#### 1.移位运算符

+  " >> " 右移位

+  " << " 左移位

+ 移位等于

  + "<<="

    + ```
      int main() {
      
          int a = 4;
      
          a >>= 1;
          printf("%d", a);// a = 2
      
          return 0;
      }
      
      >> 不会改变原来的数
      而>>=会改变原来的数
      
      ```

      + 移位等于的优先级小于算数运算符
      + "i<<2+1" 等同于 "i<<(2+1)" 而不是 "(i<<2)+1"

+  按位求反 ：~

+ 按位与：&

+ 按位异或： ^

+ 按位或: |

+ ~ 是一元运算符，其他的都是二元运算符

+ 优先级： ~ > & > ^ > |
