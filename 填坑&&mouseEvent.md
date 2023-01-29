### 1. 浅拷贝为何没有构造出crash

```bash
堆指针在被delete的时候只是表示该内存可以被回收，但是内存具体什么时候将会被回收将由操作系统决定。
```

![image-20230129230008480](/Users/yxy/workspace/MyNotes/imgs/浅拷贝.png)

```bash
delete函数的析构顺序：
  1.当前类的析构器
  2.当前类成员的析构器（按照声明顺序从后向前）
  3.基类析构器（按照继承顺序从后向前）
所以你看在delete执行之后cathy那块内存区域里面的string也是调用了stl里面的析构成为了空字符串
```

![image-20230129230852580](/Users/yxy/workspace/MyNotes/imgs/析构.png)

```bash
所以你看被释放的指针后面还是可以继续操作对应的内存区域，为了避免这种情况，delete和置空/重赋值一起用 来保证避免上面的问题
```

![image-20230129231549399](/Users/yxy/workspace/MyNotes/imgs/res.png)



