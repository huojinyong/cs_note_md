---
title: python技巧
date: 2021-05-08 19:22
---
[TOC]
- [~~判断b是不是a的子集（是子集不是真子集）~~](#判断b是不是a的子集（是子集不是真子集）)
- [Python判断某个列表是否是另一个列表的子列表](#python判断某个列表是否是另一个列表的子列表)
- [python如何在一个for循环中遍历两个列表（使用了zip 技术）](#python如何在一个for循环中遍历两个列表（使用了zip技术）)
- [把列表逆序排列](#把列表逆序排列)
- [深浅拷贝](#深浅拷贝)
  - [浅拷贝](#浅拷贝)
  - [深拷贝](#深拷贝)
- [【报错】local variable 'animal' referenced before assignment](#【报错】local-variable-animal-referenced-before-assignment)
**注意！** *在 github 中，有些目录点击后无法跳转到对应位置，这很可能是因为点击的目录内容体中含有英文所致！点击距您最近的目录，然后用鼠标滑轮前往即可！* 

# ~~判断b是不是a的子集（是子集不是真子集）~~
```python
a = ['1','2','3']
b = ['2','3']

d = [False for c in b if c not in a]
if d:
    print('b not in a')
else:
    print('b in a')
```
(好像不可行)


# Python判断某个列表是否是另一个列表的子列表
```python
ls1 = ['sa1','sa5','sa8']
ls2 = ['sa1','sa5','sa8','sa10']
set(ls1).issubset(set(ls2))
True
```
# python如何在一个for循环中遍历两个列表（使用了zip 技术）
```python
list1 = ['a', 'b', 'c', 'd']
list2 = ['apple', 'boy', 'cat', 'dog']
for x, y in zip(list1, list2):
    print(x, 'is', y)

# 输出
a is apple
b is boy
c is cat
d is dog
```

**原理说明**
Python3中的zip函数可以把两个或者两个以上的迭代器封装成生成器，这种zip生成器会从每个迭代器中获取该迭代器的下一个值，然后把这些值组装成元组（tuple）。这样，zip函数就实现了平行地遍历多个迭代器。
**注意**
如果输入的迭代器长度不同，那么，只要有一个迭代器遍历完，zip就不再产生元组了，zip会提前终止，这可能导致意外的结果，不可不察。如果不能确定zip所封装的列表是否等长，可以改用 itertools 内置模块中的zip_longest 函数，这个函数不在乎它们的长度是否相等。
在Python2中，zip不是生成器，它平行地遍历这些迭代器，组装元组，并把这些元组所构成的列表一次性完整地返回，这可能会占用大量内存并导致程序崩溃，如果在Python2中要遍历数据量大的迭代器，推荐使用 itertools 内置模块中的 izip 函数。

# 把列表逆序排列
![](./_image/2021-05-08/555image.png)
# 深浅拷贝
## 浅拷贝
python中，变量其实只是个名字、标签。也就是**浅拷贝**
```python
a = [1,2,3]
b = a
a[1] = "spam"
print("a=",a)
print("b=",b)

a = [4,5,6]

print("a=",a)
print("b=",b)

print("a的ID:",id(a))
print("b的ID:",id(b))
```
![](./_image/2021-05-08/666image.png)
a[1] = "spam"这句话改变了[1,2,3]这个列表，所以b也变了；
a = [4,5,6]这句话没有改变[1,'spam',3]这个列表，只是让a指向其他内存了。b还是指向原来的[1,'spam',3]的内存，所以b没变。

## 深拷贝
```python
a = [1,2,3]
b = a[:]
a[1] = "spam"
print("a=",a)
print("b=",b)
```
![](./_image/2021-05-08/777image.png)
上图 👆可以看到，对a进行更改并不影响b。这是因为b=a[:]是对a进行了深拷贝，即b指向了新开辟的内存。

`yellow:结论：把一个可能被改变的值（尤其是类内的值：self.XXX）赋给一个变量时，要明白该变量的值可能在你未对他进行操作时发生改变！（因为可能有其他操作改变了他指向的内存的值）`


# 【报错】local variable 'animal' referenced before assignment
**全局变量与局部变量**
报错原因是：python的函数中和全局同名的变量，如果你有修改变量的值就会变成局部变量，对该变量的引用自然就会出现没定义这样的错误了。
`yellow:结论：当函数内想访问并更改函数外的全局变量时，必须加global全局关键字！！！`
```python
x = 1
def change_x():
    gloabl x
    x = 2
```    
# 读取文件路径的反转义问题      
读取 "D:\abc\xxx.txt"之类的文件如果出现转移符号，则需要在前面加上 r，即 r"D:\abc\xxx.txt"。   
**字符串定义可以直接定义为 str = r"D:\abc\xxx.txt"**    
# 随机打乱列表   
import random   
random.shuffle(list_name)    

# pycharm 生成可执行文件   
1、打开Pycharm。   
 2、打开Terminal（快捷键Alt + F12）：View -> Tool Windows -> Terminal   
3、如果还没安装，则安装pyinstaller工具   
 输入：pip install pyinstaller   
 4、生成本项目可执行文件   
 Terminal中输入：pyinstaller -F -w main.py(你自己的 py 名字)   
