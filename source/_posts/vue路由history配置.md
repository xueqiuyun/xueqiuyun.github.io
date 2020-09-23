---
layout: 'n'
title: vue路由history模式
date: 2020-09-03 11:02:11
tags:
---
vue-router 默认是 hash 模式，在 url后面会有一个 # 号，在一些情况下，因为 #号的原因，会让后面的 uri 丢失导致 url  跳转出现问题(比如在微信内跳转异常)。这时候 可以使用 history 模式，取缔 # 号，这时候需要在服务器进行配置。  
#### nginx的一些知识点

**location**  

语法规则：location [=|~|~*|^~|@] pattern { … }  
-    =开头表示精确匹配  
-    ~ 开头表示区分大小写的正则匹配  
-    ~* 开头表示不区分大小写的正则匹配  
-    ^~ 开头表示uri以某个常规字符串 URI开头进行匹配。nginx不对url做编码，因此请求为/static/20%/aa，可以被规则^~          /static/ /aa匹配到（注意是空格）  
-    / 通用匹配，任何请求都会匹配到。  
    
**root**  
根路径配置，在匹配到 location 的 uri 路径后，指向 root 配置的路径，并把 uri 路径加在 root 路径后面。 

```
location /dist/ {
    root /home/mine/files/;
}
```  

当我访问 http://[host]/dist/test.png 时，实际上返回的文件路径为 /home/mine/files/dist/test.png  

**alias**  
别名配置，在匹配到 location 的 uri 路径后，指向 alias 配置的路径。  

```
location /dist/ {
    alias  /home/mine/files/;
}
```  

当我访问 http://[host]/dist/test.png 时，实际上返回的文件路径为 /home/mine/files/test.png

**try_files** 

try_file 的作用类似与重定向  

```
location /dist/ {
    alias /home/mine/files/;
    try_files $uri $uri/ /dist/index.html;
}
``` 
当访问 http://[host]/dist/example时，try_files 首先会在 /home/mine/files/ 目录下找是否有 example 这个文件，有则返回，未找到则找是否有 example 这个目录，有则返回，未找到则发起一个服务器内部发起重定向请求到 http://localhost/dist/index.html 

**Vue Router配置**  

当设置了 mode 为 history 时，Vue Router 有一个 base 的配置，假如 SPA 放入在一个 [host]/dist/ 服务下时，可以将 base 设置为 /dist/  
此时 nginx 的配置可以更新为： 


```
location /dist {
    alias /home/mine/files;
    index inde.html;
    try_files $uri $uri/ /dist/index.html;
}
``` 

将打包之后的代码放入 /home/mine/files 根目录下。
 


