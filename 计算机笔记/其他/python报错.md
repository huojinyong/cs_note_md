---
title: python报错
date: 2021-05-23 19:12
---

# UnicodeDecodeError: 'gbk' codec can't decode byte 0xad in position 13
问题描述：打开文件错误
解决方法：
把with open(target_word) as file_obj:  
用   
with open(target_word,'r',encoding='UTF-8') as file_obj:    
代替   
