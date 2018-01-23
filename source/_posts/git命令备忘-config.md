---
title: git命令备忘-config
date: 2018-01-18 09:28:07
tags: 
  - git
---
#### config命令：以 修改提交的用户名和邮箱 为例子
##### 添加一条配置
* 注意，添加完之后，一定要检查是否存在多条user.name user.email的记录
* 如果希望所有的git仓库都可以使用到： 

 ``` 
	git config --global --add user.email "myaddress@gmail.com"  
	git config --global --add user.name "myname"
 ```

 这样设置之后，本机任何的git提交author 为myname。  
在任何仓库下使用git log 查看，会显示  

 ```
	Author: myname <myaddress@gmail.com>
 ```
 
* 如果希望当前仓库使用特定的用户名邮箱:  
首先切换到要修改的仓库目录下  

 ```
	git config --local --add user.email "myaddressLocal@gmail.com"  
	git config --local --add user.name "mynameLocal"  
 ```

 这样设置之后，该仓库的git提交author 为mynameLocal。  
在该仓库下使用git log 查看，会显示

 ```
	Author: mynameLocal <myaddressLocal@gmail.com>
 ```

 其他仓库的git提交author 依然为myname。  
在该仓库下使用git log 查看，依然会显示  
 
 ```
 	Author: myname <myaddress@gmail.com>
 ```
		 
##### 查看配置
	
* 查看全局配置  

 ```
	git config --global --list
 ```
	
* 查看当前仓库的配置  
首先切换到要修改的仓库目录下  

 ```
	git config --local --list
 ```

##### 删除配置
	
* 删除全局配置  
 
 ```
  git config --global --unset user.name  
  git config --global --unset user.email
 ```

 如果有多条记录，会提示warning: user.name has multiple values，这个时候就需要加正则表达式就行过滤。例如，原来有两条user.name的记录

 ```
  user.name=fengfeng
  user.name=tte
 ```

 如果想删除tte的记录
 
 ```
  git config --global --unset user.name tt*
 ```

* 删除当前仓库的配置  
首先切换到要修改的仓库目录下  

 ```
  将上述全局的--global 替换为 --local执行
 ```

##### 编辑配置
* 全局命令修改：  

 ```
  git config --global user.email "myaddress@gmail.com"  
  git config --global  user.name "myname"
 ```

 如果有多条记录，会提示cannot overwrite multiple values with a single value，这个时候就需要加正则表达式就行过滤。例如，原来有两条user.name的记录
 
 ```
  user.name=fengfeng
  user.name=tte
 ```

 想要把tte修改为myname，则应该执行
 
 ```
  git config --global user.name myname tt*
 ```
 
* 当前仓库命令修改

 ```
	将上述全局的--global 替换为 --local执行
 ```
 
* 编辑器修改  
会打开vim编辑器   
全局：

 ```
	git config --global -e
 ```
 仓库：
 
 ```
 	git config --local -e  
 ```

	 
