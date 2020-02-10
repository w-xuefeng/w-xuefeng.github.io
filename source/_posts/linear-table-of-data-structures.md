---
title: 数据结构之单链表
date: 2018-04-01 12:00:00
categories: 技术贴 | 数据结构
tags: DataStructures
thumbnail: https://pub.wangxuefeng.com.cn/asset/blogthumbnail/linearTableOfDataStructures/thumbnail.png
---
### 单链表节点类型定义

```c
	typedef int DataType; //定义数据类型，此处以整型为例
	typedef struct node{
		DataType data; //节点的数据域
		struct node *next; //节点的指针域
	}NODE,*LinkList;
```

### 单链表的运算函数

#### 查找

```c

	/**
	*
	* @function 在表中查找第k个元素，若找到，返回该元素节点的指针；否则返回空指针NULL
	* @parameter L 带头节点单链表的头指针
	* @parameter k 要查找元素的位置
	* @return 查找到元素节点的指针或者空指针NULL
	*
	*/

	LinkList Find_List(LinkList L, int k){
		LinkList p = L->next; //令p指向第一个元素
		int i = 1; //初始化计数器
		while(p && i < k ){ //依次向后查找，直到p指向第k个元素节点或者p为空指针
			p = p->next;
			i++;
		}
		return (p && i==k) ? p : NULL;
	}

```

#### 插入

```c

	/**
	*
	* @function 将元素newElem插入表中的第k个元素之前即第k-1个元素之后,成功返回0，失败返回-1
	* @parameter L 带头节点单链表的头指针
	* @parameter k 要插入元素的位置
	* @parameter newElem 要插入的新元素
	* @return 0或-1
	*
	*/

	int Insert_List(LinkList L, int k, DataType newElem){
		LinkList p, s; //临时指针
		p = (k == 1)? L : Find_List(L, k-1);
		if(!p) return -1; //表中不从在第k-1个元素
		s = (NODE*)malloc(sizeof(NODE)); //为新元素申请节点空间
		if(!s) return -1; //空间申请失败
		s->data = newElem;
		s->next = p->next;
		p->next = s; //插入元素
		return 0;
	}

```

#### 删除

```c

	/**
	*
	* @function 删除表中的第k个元素节点，即将第k-1个元素的指针域指向第k+1个元素所在节点，成功返回0，失败返回-1
	* @parameter L 带头节点单链表的头指针
	* @parameter k 要删除元素的位置
	* @return 0或-1
	*
	*/

	int Delete_List(LinkList L, int k){
		LinkList p, q; //临时指针
		p = (k == 1)? L : Find_List(L, k-1);
		if(!p || !p->next) return -1; //表中不从在第k个元素
		q = p->next;
		p->next = q->next;
		free(q); //删除节点
		return 0;
	}

```