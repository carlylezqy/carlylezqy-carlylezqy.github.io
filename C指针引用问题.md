```cpp
void GetMemory( char*p )
{
  p = (char*) malloc( 100 );
}
void Test( void ) 
{
  char*str = NULL;
  GetMemory( str ); 
  strcpy( str, "hello world" );
  printf( str );
}
```

如图所示，Test函数执行时，str指向NULL。

![img](https://pic1.zhimg.com/80/ceb7b9df9738211da36ef3ce43d3ff38_1440w.jpg?source=1940ef5c)


后经过GetMemory函数后，发生了一次赋值，即 char *p = str; p指向了（str指向的NULL），于是就变为了如此

![img](https://pic3.zhimg.com/80/d290d8df9046589d44a3a9b4e6c5a86d_1440w.jpg?source=1940ef5c)

然而经过了GetMemory的malloc以后，p获得了一块新内存的地址，于是p的指向就发生了改变。

![img](https://pic1.zhimg.com/80/356b9f4a5f54f49ef3885d7e54a782fa_1440w.jpg?source=1940ef5c)

那么，从这里可以看出来str与p指向区域已经发生改变，而str也还是指向NULL。



那么，解决的方法是：

1. 使用C++的引用
2. 二重指针，即把 GetMemory 变为 GetMemory(char ** p) 来保存str的地址。

# 二重指针

一重指针变量和二重指针变量本身都占4字节内存空间，本质都是指针变量。

他们的区别是：二重指针指向的区域须为一个一重指针。