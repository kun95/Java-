# 如何使用gitbook来写书

## 准备

- 安装git


- 安装node

- 安装gitbook

  ```bash
  cnpm install gitbook-cli -g #安装gitbook
  gitbook -V #查看安装后的版本
  ```



## 理论基础

- gitbook基本命令

  ```bash
  gitbook serve . #启动gitbook服务，服务默认启动在4000端口
  gitbook help #查看gitbook命令
  gitbook init #初始化gitbook目录
  ```

- SUMMARY.md与README.md

  当执行gitbook init之后，会在当前目录下生成这两个文件，其中

  README.md 相当于这本书的说明/前言

  SUMMARY.md 相当于这本书的目录

- SUMMARY.md结构

  ```
  * [前言](README.md)
  * [Idea](idea/readme.md)
  * [Eclipse](eclipse/readme.md)
  * [Gitbook](gitbook/readme.md)
    - [使用gitbook写书](gitbook/how-to-use-gitbook.md)
  * [Bash](bash/readme.md)
    - [设置bash自定义命令](bash/alias.md)
  ```

  通过这种定义，gitbook便可以通过读取SUMMARY.md来生成图书的章节 

## 实战

目的：想建立一本书，用来记录工作中遇到的各种软件的使用方法

步骤：

1. 安装好必备的软件
2. 选择一个目录，cd到该目录中，执行gitbook init命令
3. 编辑init命令生成的README.md文件，填写一些书籍说明
4. 编辑init命令生成的SUMMARY.md文件，填写书籍目录，可以参考上面SUMMARY.md的写法
5. 编辑指定文章对应的md文件
6. `gitbook serve .`启动gitbook，注意要在项目的根目录下执行，.代表当前目录，意思是说，在当前目录下启动gitbook，此时gitbook就会去读取当前目录下的SUMMARY.md文件等，并生成目录，以及通过SUMMARY.md目录中的定义，建立章节与内容的关联
7. 访问 http://localhost:4000 便可以查看到你编写的书籍

## 推送到gitbook

1. 使用 git init 初始化当前目录为一个git仓库

2. 使用 git remote add gitbook https://git.gitbook.com/kun95/java-relearn.git 来添加远程仓库地址

3.  使用git add将之前写的文件加入到git版本控制

4. 使用git commit -m 'xxx' 提交到git版本控制

   xxx为本次提交的注释

5. 使用git push gitbook master 将本地当前分支推送到远程仓库master分支

## 推送到github

步骤同上

## 最佳实践

通过实验，最方便的步骤应该是：

1. 配置好本地环境
2. github上创建一个仓库
3. 将书籍push到github仓库上
4. 到gitbook上创建一个仓库，注意创建的时候选择从github上导入，此时会让你填写书名以及选择github仓库
5. 在本地写，写完之后推送到github ，推送之后，gitbook也会同步更新，到gitbook中就能看到最新的书籍