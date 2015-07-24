---
layout: post
title: Full Stack Foundation Using Python 1
---

Python 全栈基础
===
<br>
最近在看Udacity上的 [Full Stack Foundations](https://www.udacity.com/course/viewer#!/c-ud088/)，从基础的CRUD开始介绍使用Python构建Web应用的各项步骤。本系列文章将介绍该课程所讲的内容，也算是我的笔记。
<br>
##Working with CRUD##

###什么是CRUD

- C - **Create**
- R - **Read**
- U - **Update**
- D - **Delete**

他们分别对应数据库的四个操作是

- **insert**
- **select**
- **update**
- **delete**

###ORM
一般来说，我们如果要对数据库进行操作，需要使用SQL语句。而ORM则是使数据库中的表与Python中的类相对应。

例如我们现在需要做一个餐馆的网页，用来显示每家餐馆的菜单，那么我们就需要一个餐馆的表。

例如最简单的，只有id和name两个属性：

属性|类型
---|---
Id | Integer
Name | String(250)

那么我们就可以使用ORM将它转化为一个类：

```python
calss Restaurant:
	__tablename__ = "restaurant"
	id = Column(Integer, primary_key = True)
	name = Column(String(250), nullable = False)
```

他们之间的关系可以用下图描述
![Image of ORM](/images/database-orm-python.jpg)


###使用SQLAlchemy实现CRUD

**SQLAlchemy**是一个pythonORM库，具体可以看官网的文档。这里只说用到的。

首先我们需要创建数据库

1. 配置代码
	```python
	import sys
	from sqlalchemy import Column, ForeignKey, Integer, String
	from sqlalchemy.ext.declarative import declarative_base
	from sqlalchemy.orm import relationship
	from sqlalchemy import create_engine

	Base = declarative_base()

	```
2. 创建类

	都要继承自Base，Restaurant表示餐馆
	```python
	class Restaurant(Base):
	```

3. 定义Table名称

	```python
	__tablename__ = "restaurant"
	```

4. 描述对应关系

	``` python
	id = Column(Integer, primary_key = True)
	name= Column(String(250), nullable = False)
	```

5. 最后创建数据库代码

	```python
	engine = create_engine('sqlite:///restaurantmenu.db')
	Base.metadata.create_all(engine)
	```
6. 整体代码

	```python
	import sys
	from sqlalchemy import Column, ForeignKey, Integer, String
	from sqlalchemy.ext.declarative import declarative_base
	from sqlalchemy.orm import relationship
	from sqlalchemy import create_engine
	
	Base = declarative_base()
	
	class Restaurant(Base):
		__tablename__ = "restaurant"
		id	=	Column(Integer, primary_key	=	True)
		name=	Column(String(250), nullable=	False)
	
	class MenuItem(Base):
		__tablename__ = "menuitem"
		name=	Column(String(80), nullable=	False)
		id	=	Column(Integer, primary_key=	True)
		description= Column(String(250))
		price = Column(String(8))
		course = Column(String(250))
		restaurant_id = Column(Integer, ForeignKey('restaurant.id'))
		restaurant = relationship('Restaurant')
	
	engine = create_engine('sqlite:///restaurantmenu.db')
	Base.metadata.create_all(engine)
	```

其中relation描述了外键属性

运行此代码后即可生成sqlite文件。


###CRUD操作代码实现

我们可以直接在python解释器中运行代码

