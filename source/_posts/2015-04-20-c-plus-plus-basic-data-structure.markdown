---
layout: post
title: "c++ basic data structure"
date: 2015-04-20 22:04:11 -0400
comments: true
categories: c++ algorithm
---

###basic data structure and algorithm
####little review about c++ object oriented
- 虚函数
    - 核心理念就是基类访问派生类定义的函数
    - 动态联编
    - 一个函数的调用不是在编译的时候确定的，而是在运行的时候确定的，并且因为写代码的时候不能确定被调用的函数是基类的函数还是派生类的函数，所以这个函数又叫做“虚函数“
```
    class A{
        public:
            virtual void test(){
                cout<<"A:test() is called";
            }        
    };
    class B: public A{
        public:
            virtual void test(){
                cout<<"B:test() is called";
            }
    };
    int main(){
        A *a = new B();
        a -> test();
    }
```
    
<!--more-->
- 虚函数表
    - 实现多态的主要功能
    - 编译器会为每一个有虚函数的类的实例创建一个虚函数表 
    - 用来存虚函数的table
        - table的每个slot（槽）里面存放虚函数的地址

- 纯虚函数
    - `virtual void test() = 0`
    - 意思是抽象类，也可以说是接口，用来规范派生类的行为
        - 告诉使用者我的派生类都会有这个函数
    - 虚构析函数
        - 当一个类要被其他的类当基类使用的时候，必须是纯虚的
        - 如果有两个class A和B
            - B继承A，但是A的构析函数没有设置成虚函数
            - 那么在delete B的实例的时候，只有A的实例被delete， B的不会被delete。。。那这不是坑爹吗。。。。
            - 但是再A的构析函数前面加上virtual，这样就能保证在delete B的实例的时候，两个类的构析函数都会被调用
            
- 但是构造函数不能使虚函数

-----------------------------------

####链表
- 链表ADT
```
template <typename E> class List{
	private:
		void operator = (const List &){}
		List(const List&){}
	public:
		List(){}
		virtual ~List(){}
		virtual void clear() = 0;
		virtual void insert(const E& item) = 0;
		virtual void append(const E& item) = 0;
		virtual E remove() = 0;
		//move the pointer to start
		virtual void moveToStart() = 0;
		//move the pointer to end
		virtual void moveToEnd() = 0;
		virtual void prev() = 0;
		virtual void next() = 0;
		virtual int length() const = 0;
		virtual int currPos() const = 0;
		virtual void moveToPos(int pos) = 0;
		virtual const E& getValue() const = 0;
};
```

-----------------------------------

- 数组实现
```
    template <typename E> class AList: public List<E>{
	private:
		int maxSize;
		int listSize;
		int curr;
		E* listArray;	
	public:
	    //初始化列表
		AList(int size = 100){
			maxSize = size;
			listSize = 0;
			curr = 0;
			listArray = new E[maxSize];
		}
		//构析函数，删掉数组，释放空间
		~AList(){
			delete []listArray;
		}
		void clear(){
			delete []listArray;
			listSize = 0;
			curr = 0;
			listArray = new E[maxSize];
		}
		//把当前位置之后的数组向后移动一位，再插入
		void insert(const E& it){
			for(int i = listSize; i > curr; i--)
				listArray[i] = listArray[i-1];
			//move back the array from the current position
			listArray[curr] = it;
			listSize++;
		}
		//直接在最后增加item
		void append(const E& it){
			listArray[listSize++] = it;
		}
		//记录当前的数组索引的指向的数据，把数组向前移动一位
		E remove(){
			E it = listArray[curr];
			for(int i = curr; i < listSize - 1; i++){
				listArray[i] = listArray[i + 1];
			}
			listSize--;
			return it;
		}
		void moveToStart(){
			curr = 0;
		}
		void moveToEnd(){
			curr = listSize;
		}
		void prev(){
			if(curr > 0)
				curr--;
		}
		void next(){
			if(curr < listSize)
				curr++;
		}
		int length(){
			return listSize;
		}
		int currPos() const{
			return curr;
		}
		void moveToPos(int pos){
			pos = curr;
		}
		const E& getValue() const{
			return listArray[curr];
		}
    };
```

-----------------------------------
    
- 链式实现
```
    template <typename E> class Link{
	public:
		E element;
		Link *next;
		Link(const E& elemval, Link *nextval = NULL){
			element = elemval;
			next = nextval;
		}
		Link(Link *nextval = NULL){
			next = nextval;
		}
};
template <typename E> class LList: public List<E>{
	private:
		Link<E> *head;
		Link<E> *tail;
		Link<E> *curr;
		int count;
		void init(){
			curr = tail = head = new Link<E>;
			count = 0;
		}
		void removeall(){
			while(head != NULL){
				curr = head;
				head = head -> next;
				delete curr;
			}
		}
	public:
		LList(int size=100){
			init();
		}
		~LList(){
			removeall();
		}
		void clear(){
			removeall();
			init();
		}
		void insert(const E& it){
			//给要增加的节点初始化
			curr -> next = new Link<E>(it, curr -> next);
			//如果要curr指针就是再末尾
			//那么把curr的下一个赋给tail
			if(tail == curr)
				tail = curr -> next;
			count++;
		}
		void append(const E& it){
			//直接把末尾指针的next指向新建的link
			tail = tail -> next = new Link<E>(it, NULL);
			count++;
		}
		//注意，这里要删除的节点叫做curr->next
		E remove(){
			//先把要删除的node的值存起来
			E it = curr -> next -> element;
			//用temp存一下要删除的节点
			Link<E> *temp = curr -> next;
			//如果这个要删除的点是末尾，那么把末尾前一个节点赋给tail
			if(tail == curr -> next)
				tail = curr;
			//否则，把要删除的节点的前一个节点的next指向要删除节点的下一个
			curr -> next = curr -> next -> next;
			delete temp;
			count--;
			return it;
		}
		void moveToStart(){
			curr = head;
		}
		void moveToEnd(){
			curr = tail;
		}
		void prev(){
			if(curr == head)
				return ;
			Link<E> *temp = head;
			//向左移动一个单位
			//做法是先用temp存一个head，然后向右找，直到找到curr的前一个，然后把curr的前一个赋给curr
			while(temp -> next != curr)
				temp = temp -> next;
			curr = temp;
		}
		void next(){
			//只要curr指针不是tail，那么就向后移动
			if(curr != tail)
				curr = curr -> next;
		}
		int length(){
			return count;
		}
		int currPos() const{
			Link<E> *temp = head;
			//用temp指针存head，然后依次向后遍历，并且每次后移count+1
			int i;
			for(i = 0; i < count; i++){
				temp = temp -> next;
			}
			return i;
		}
		void moveToPos(int pos){
			curr = head;
			//先把current的指针指向head
			//然后一直向后移动，直到pos次
			for(int i = 0; i < pos; i++){
				curr = curr -> next;
			}
		}
		const E& getValue() const{
			return curr -> next -> element;
		}
    };
```

-----------------------------------
    
####栈
- 数组实现
```
class Astack{
	private:
		int maxSize;
		int top;
		int *array;
	public:
		Astack(int size = 100){
			maxSize = size;
			top = 0;
			array = new int[size];
		}
		~Astack(){
			delete []array;
		}
		void clear(){
			top = 0;
		}
		void push(int item){
			array[top++] = item;
		}
		int pop(){
			int temp = array[top];
			return array[--top];
		}
		int getTop(){
			return array[top - 1];
		}	
};
int main(){
	Astack a;
	a.push(1);
	cout<<a.getTop();
	a.pop();
	cout<<a.getTop();
	return 0;
}
```
-----------------------------------
####队列
- 数组实现
```
class Aqueue{
	private:
		int front;
		int rear;
		int maxSize;
		int *array;
	public:
		Aqueue(int size = 100){
			maxSize = size;
			front = rear = 0;
			array = new int[size];
		}
		~Aqueue(){
			delete [] array;
		}
		void enqueue(int item){
			array[rear] = item;
			rear = (rear + 1)%maxSize;
		}
		int dequeue(){
			int temp = array[front];
			front = (front + 1)%maxSize;
			array[front] = 0;
			return temp;
		}
		const int getFrontValue(){
			return array[front];
		}
};
int main(){
	Aqueue q;
	q.enqueue(1);
	cout<<q.getFrontValue()<<endl;
	q.dequeue();
	cout<<q.getFrontValue();
	return 0;
}
```

####二叉树
- 遍历
    - 前序遍历
```
        void preorder(Node *root){
            if(root == NULL){
                return ;
            }
            cout<<root->value;
            preorder(root -> left);
            preorder(root -> right);
        }
```
    - 中序遍历
```
        void inorder(Node *root){
            if(root == NULL){
                return ;
            }
            inorder(root -> left);
            cout<<root -> value;
            inorder(root -> right);
        }
```
    - 后序遍历
```
        void postorder(Node *root){
            if(root == NULL){
                return ;
            }
            postorder(root -> left);
            postorder)root -> right);
            cout<<root -> value;
        }
```