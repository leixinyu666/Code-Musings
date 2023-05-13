# STL
一、STL概念



STL分为六大组件，分别是:容器、算法、迭代器、仿函数、适配器（配接器）、空间配置器

1. 容器：各种数据结构，如vector、list、deque、set、map等,用来存放数据。
2. 算法：各种常用的算法，如sort、find、copy、for_each等
3. 迭代器：扮演了容器与算法之间的胶合剂。
4. 仿函数：行为类似函数，可作为算法的某种策略。
5. 适配器：一种用来修饰容器或者仿函数或迭代器接口的东西。
6. 空间配置器：负责空间的配置与管理。



二、STL容器



2.1 string容器：字符串



构造函数

        string s1; //创建空字符串，调用无参构造函数
    
    	const char* str = "hello world";
    	string s2(str); //把c_string转换成了string
    
    	string s3(s2); //调用拷贝构造函数
    
    	string s4(10, 'a');//10个a



赋值

        string str1;
    	str1 = "hello world";
    
    	string str2;
    	str2 = str1;
    
    	string str3;
    	str3 = 'a';

用 “=” 操作符



拼接

        string str1 = "我";
    	str1 += "爱玩游戏";
    	str1 += ':';
    
    	string str2 = "LOL DNF";
    	str1 += str2;

用 “+=” 操作符



查找替换

        //查找
    	string str1 = "abcdefgde";
    
    	int pos = str1.find("de");  //左边开始第一次出现的下标
    
    	if (pos == -1)
    	{
    		cout << "未找到" << endl;
    	}
    	else
    	{
    		cout << "pos = " << pos << endl;
    	}
    	
    	pos = str1.rfind("de");  //右边开始第一次出现的下标
    
    	cout << "pos = " << pos << endl;
    
        //替换
    	string str1 = "abcdefgde";
    	str1.replace(1, 3, "1111");   //1号位置开始找，替换3个长度，用1111代替
    
    	cout << "str1 = " << str1 << endl;

查找用find和rfind，替换用replace

- find查找是从左往后，rfind从右往左
- find找到字符串后返回查找的第一个字符位置，找不到返回-1
- replace在替换时，要指定从哪个位置起，多少个字符，替换成什么样的字符串



比较

        string s1 = "hello";
    	string s2 = "aello";
    
    	int ret = s1.compare(s2);
    
    	if (ret == 0) {
    		cout << "s1 等于 s2" << endl;
    	}
    	else if (ret > 0)
    	{
    		cout << "s1 大于 s2" << endl;
    	}
    	else
    	{
    		cout << "s1 小于 s2" << endl;
    	}

比较用compare

字符串对比主要是用于比较两个字符串是否相等，判断谁大谁小的意义并不是很大



存取

        string str = "hello world";
    
    	for (int i = 0; i < str.size(); i++)
    	{
    		cout << str[i] << " ";
    	}
    	cout << endl;
    
    	str[0] = 'x';
    	cout << str << endl;

访问用 ”[]“，串长度用size



插入删除

        string str = "hello";
    	str.insert(1, "111");  //1号位置插入111
    	cout << str << endl;
    
    	str.erase(1, 3);  //从1号位置开始删除3个字符
    	cout << str << endl;

插入用insert,删除用erase



子串

        string str = "abcdefg";
    	string subStr = str.substr(1, 3);  //1号位置开始截取三个
    	cout << "subStr = " << subStr << endl;
    
    	string email = "hello@sina.com";
    	int pos = email.find("@");           //先find查找得下标，在截取长度
    	string username = email.substr(0, pos);
    	cout << "username: " << username << endl;

子串用substr

不知截取的具体长度，先find找到对应终止符的下标，再用substr截取



2.2 vector容器：数组（单端）

单端数组，动态拓展（并不是在原空间之后续接新空间，而是找更大的内存空间，然后将原数据拷贝新空间，释放原空间）



打印函数

    void printVector(vector<int>& v) {
    
    	for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
    		cout << *it << " ";
    	}
    	cout << endl;
    }



构造函数

        vector<int> v1; //无参构造
    	for (int i = 0; i < 10; i++)
    	{
    		v1.push_back(i);
    	}
    	printVector(v1);
    
    	vector<int> v2(v1.begin(), v1.end());
    	printVector(v2);
    
    	vector<int> v3(10, 100);  //10个100
    	printVector(v3);
    	
    	vector<int> v4(v3);   //拷贝构造
    	printVector(v4);



赋值

        vector<int> v1; //无参构造
    	for (int i = 0; i < 10; i++)
    	{
    		v1.push_back(i);
    	}
    	printVector(v1);
    
    	vector<int>v2;
    	v2 = v1;
    	printVector(v2);

用 “=” 进行赋值



容量大小

        vector<int> v1;
    	for (int i = 0; i < 10; i++)
    	{
    		v1.push_back(i);
    	}
    	printVector(v1);
    
    	if (v1.empty())
    	{
    		cout << "v1为空" << endl;
    	}
    	else
    	{
    		cout << "v1不为空" << endl;
    		cout << "v1的容量 = " << v1.capacity() << endl;
    		cout << "v1的大小 = " << v1.size() << endl;
    	}
    
        //resize 重新指定大小 ，若指定的更大，默认用0填充新位置，可以利用重载版本替换默认填充
    	v1.resize(15,10);
    	printVector(v1);
    
    	//resize 重新指定大小 ，若指定的更小，超出部分元素被删除
    	v1.resize(5);
    	printVector(v1);

- 判断是否为空  --- empty
- 返回元素个数  --- size
- 返回容器容量  --- capacity
- 重新指定大小  ---  resize
                                 resize(100),多的用0填充
                                 resize(100,5),多的用5填充
                                 resize(10),删去多余的



插入删除

        vector<int> v1;
    	//尾插
    	v1.push_back(10);
    	v1.push_back(20);
    	v1.push_back(30);
    	v1.push_back(40);
    	v1.push_back(50);
    	printVector(v1);
    	//尾删
    	v1.pop_back();
    	printVector(v1);
    	//插入
    	v1.insert(v1.begin(), 100);
    	printVector(v1);
    
    	v1.insert(v1.begin(), 2, 1000);  //2个1000
    	printVector(v1);
    
    	//删除
    	v1.erase(v1.begin());
    	printVector(v1);
    
    	//清空
    	v1.erase(v1.begin(), v1.end());
    	v1.clear();
    	printVector(v1);

单向数组，只能从尾部操作

- 尾插  --- push_back
- 尾删  --- pop_back
- 插入  --- insert    (位置迭代器)
- 删除  --- erase  （位置迭代器）
- 清空  ---  clear  



存取

        vector<int>v1;
    	for (int i = 0; i < 10; i++)
    	{
    		v1.push_back(i);
    	}
    
    	for (int i = 0; i < v1.size(); i++)
    	{
    		cout << v1[i] << " ";
    	}
    	cout << endl;
    
    	cout << "v1的第一个元素为： " << v1.front() << endl;
    	cout << "v1的最后一个元素为： " << v1.back() << endl;

用[]进行访问

- front返回容器第一个元素
- back返回容器最后一个元素



互换容器

    	//互换容器
    	cout << "互换后" << endl;
    	v1.swap(v2);
    	printVector(v1);
    	printVector(v2);
    
        //真正的应用——收缩内存
        vector<int>(v).swap(v); //匿名对象

用swap交换，用vector<int>(v).swap(v)收缩内存



预留空间

        v.reserve(100000);
    
        int num = 0;
    	int* p = NULL;
    	for (int i = 0; i < 100000; i++) {
    		v.push_back(i);
    		if (p != &v[0]) {
    			p = &v[0];
    			num++;
    		}
    	}

如果数据量较大，可以一开始利用reserve预留空间



2.3 deque容器：数组（双端）

双端数组，动态拓展（deque内部有个中控器，维护每段缓冲区中的内容，缓冲区中存放真实数据，中控器维护的是每个缓冲区的地址，使得使用deque时像一片连续的内存空间）

实际上不是连续的内存空间，不像vector容器



打印函数

    void printDeque(deque<int>& d) {
    
    	for (deque<int>::iterator it = d.begin(); it != d.end(); it++) {
    		cout << *it << " ";
    	}
    	cout << endl;
    }



构造函数

        deque<int> d1; //无参构造函数
    	for (int i = 0; i < 10; i++)
    	{
    		d1.push_back(i);
    	}
    	printDeque(d1);
    
    	deque<int> d2(d1.begin(),d1.end());
    	printDeque(d2);
    
    	deque<int>d3(10,100);
    	printDeque(d3);
    
    	deque<int>d4 = d3;
    	printDeque(d4);



赋值

        deque<int> d1;
    	for (int i = 0; i < 10; i++)
    	{
    		d1.push_back(i);
    	}
    	printDeque(d1);
    
    	deque<int>d2;
    	d2 = d1;
    	printDeque(d2);

“=”



大小

        deque<int> d1;
    	for (int i = 0; i < 10; i++)
    	{
    		d1.push_back(i);
    	}
    	printDeque(d1);
    
    	//判断容器是否为空
    	if (d1.empty()) {
    		cout << "d1为空!" << endl;
    	}
    	else {
    		cout << "d1不为空!" << endl;
    		//统计大小
    		cout << "d1的大小为：" << d1.size() << endl;
    	}
    
    	//重新指定大小
    	d1.resize(15, 1);
    	printDeque(d1);
    
    	d1.resize(5);
    	printDeque(d1);

empty,size,resize

deque没有容量的概念



插入删除

        deque<int> d;
    	//尾插
    	d.push_back(10);
    	d.push_back(20);
    	//头插
    	d.push_front(100);
    	d.push_front(200);
    	//尾删
    	d.pop_back();
    	//头删
    	d.pop_front();
    
        d.insert(d.begin(), 1000);
    	printDeque(d);
    	d.insert(d.begin(), 2,10000);
    	printDeque(d);
    
        d.erase(d.begin());
    	printDeque(d);
    
    	d.erase(d.begin(), d.end());
    	d.clear();
    	printDeque(d);

- 插入和删除提供的位置是迭代器！
- 尾插   ---  push_back
- 尾删   ---  pop_back
- 头插   ---  push_front
- 头删   ---  pop_front

vector容器只能尾插尾删，deque可以头尾插删



存取

        deque<int> d;
    	d.push_back(10);
    	d.push_back(20);
    	d.push_front(100);
    	d.push_front(200);
    
    	for (int i = 0; i < d.size(); i++) {
    		cout << d[i] << " ";
    	}
    
        cout << "front:" << d.front() << endl;
    
    	cout << "back:" << d.back() << endl;

用[]访问元素



排序

不是内置函数，是算法，和vector通用，要包含算法头文件

        deque<int> d;
    	d.push_back(10);
    	d.push_back(20);
    	d.push_front(100);
    	d.push_front(200);
    
    	printDeque(d);
    	sort(d.begin(), d.end());
    	printDeque(d);

sort(d.begin(), d.end());



2.4 stack容器：栈



常用接口

        //创建栈容器 栈容器必须符合先进后出
    	stack<int> s;
    
    	//向栈中添加元素，叫做 压栈 入栈
    	s.push(10);
    	s.push(20);
    	s.push(30);
    
    	while (!s.empty()) {
    		//输出栈顶元素
    		cout << "栈顶元素为： " << s.top() << endl;
    		//弹出栈顶元素
    		s.pop();
    	}
    	cout << "栈的大小为：" << s.size() << endl;

- 入栈   --- push
- 出栈   --- pop
- 返回栈顶   --- top
- 判断栈是否为空   --- empty
- 返回栈大小   --- size



2.5 queue容器:队列



常用接口

    //创建队列
    	queue<Person> q;
    
    	//准备数据
    	Person p1("唐僧", 30);
    	Person p2("孙悟空", 1000);
    	Person p3("猪八戒", 900);
    	Person p4("沙僧", 800);
    
    	//向队列中添加元素  入队操作
    	q.push(p1);
    	q.push(p2);
    	q.push(p3);
    	q.push(p4);
    
    	//队列不提供迭代器，更不支持随机访问	
    	while (!q.empty()) {
    		//输出队头元素
    		cout << "队头元素-- 姓名： " << q.front().m_Name 
                  << " 年龄： "<< q.front().m_Age << endl;
            
    		cout << "队尾元素-- 姓名： " << q.back().m_Name  
                  << " 年龄： " << q.back().m_Age << endl;
            
    		cout << endl;
    		//弹出队头元素
    		q.pop();
    	}
    
    	cout << "队列大小为：" << q.size() << endl;

- 入队   --- push
- 出队   --- pop
- 返回队头元素   --- front
- 返回队尾元素   --- back
- 判断队是否为空   --- empty
- 返回队列大小   --- size



2.6 list容器：链表

双向循环链

STL中List和vector是两个最常被使用的容器，各有优缺点（数组和链表，顺序表和链表）



打印函数

    void printList(const list<int>& L) {
    
    	for (list<int>::const_iterator it = L.begin(); it != L.end(); it++) {
    		cout << *it << " ";
    	}
    	cout << endl;
    }



构造函数

        list<int>L1;
    	L1.push_back(10);
    	L1.push_back(20);
    	L1.push_back(30);
    	L1.push_back(40);
    
    	printList(L1);
    
    	list<int>L2(L1.begin(),L1.end());
    	printList(L2);
    
    	list<int>L3(L2);
    	printList(L3);
    
    	list<int>L4(10, 1000);
    	printList(L4);



赋值交换

    	//赋值
    	list<int>L2;
    	L2 = L1;
    	printList(L2);
    
        //交换
        L1.swap(L2);

赋值用=，交换用swap



大小

        list<int>L1;
    	L1.push_back(10);
    	L1.push_back(20);
    	L1.push_back(30);
    	L1.push_back(40);
    
    	if (L1.empty())
    	{
    		cout << "L1为空" << endl;
    	}
    	else
    	{
    		cout << "L1不为空" << endl;
    		cout << "L1的大小为： " << L1.size() << endl;
    	}
    
    	//重新指定大小
    	L1.resize(10);
    	printList(L1);
    
    	L1.resize(2);
    	printList(L1);

- 判断是否为空   --- empty
- 返回元素个数   --- size
- 重新指定个数   --- resize



插入删除

    list<int> L;
    	//尾插
    	L.push_back(10);
    	L.push_back(20);
    	L.push_back(30);
    
    	//头插
    	L.push_front(100);
    	L.push_front(200);
    	L.push_front(300);
    
    	//尾删
    	L.pop_back();
    
    	//头删
    	L.pop_front();
    
    	//插入
    	list<int>::iterator it = L.begin();
    	L.insert(++it, 1000);
    
    	//删除
    	it = L.begin();
    	L.erase(++it);
    
    	//移除
    	L.push_back(10000);
    	L.push_back(10000);
    	L.push_back(10000);
    	L.remove(10000);
        
        //清空
    	L.clear();

- 尾插   --- push_back
- 尾删   --- pop_back
- 头插   --- push_front
- 头删   --- pop_front
- 插入   --- insert
- 删除   --- erase
- 移除   --- remove
- 清空   --- clear



存取

        list<int>L1;
    	L1.push_back(10);
    	L1.push_back(20);
    	L1.push_back(30);
    	L1.push_back(40);
    
    	
    	//cout << L1.at(0) << endl;//错误 不支持at访问数据
    	//cout << L1[0] << endl; //错误  不支持[]方式访问数据
    	cout << "第一个元素为： " << L1.front() << endl;
    	cout << "最后一个元素为： " << L1.back() << endl;
    
    	//list容器的迭代器是双向迭代器，不支持随机访问
    	list<int>::iterator it = L1.begin();
    	//it = it + 1;//错误，不可以跳跃访问，即使是+1

不能随机访问，只能通过front和back访问头尾元素



反转和排序

    	//反转容器的元素
    	L.reverse();
    	printList(L);
    
    	//排序
    	L.sort(); //默认的排序规则 从小到大
    	printList(L);
    
    	L.sort(myCompare); //指定规则，从大到小
    	printList(L);
    
        L.sort(ComparePerson); //排序

- 反转   --- reverse
- 排序   --- sort （成员函数）默认从小到大，从大到小需要自定义

    bool myCompare(int val1 , int val2)
    {
    	return val1 > val2;
    }
    
    bool ComparePerson(Person& p1, Person& p2) {
    	if (p1.m_Age == p2.m_Age) {
    		return p1.m_Height  > p2.m_Height;
    	}
    	else
    	{
    		return  p1.m_Age < p2.m_Age;
    	}
    
    }

    return val1 > val2——从大到小



    if (p1.m_Age == p2.m_Age) {
		return p1.m_Height  > p2.m_Height;——年龄相同，身高从大到小
	}
	else
	{
		return  p1.m_Age < p2.m_Age;——年龄不同，年龄从小到大
	}



2.7 set容器：二叉排序树

所有元素都会在插入时自动被排序，按照从小到大自动排序

set不允许容器中有重复的元素，输入两个相同的只会显示一个

multiset允许容器中有重复的元素



底层：二叉排序树



打印函数

    void printSet(set<int> & s)
    {
    	for (set<int>::iterator it = s.begin(); it != s.end(); it++)
    	{
    		cout << *it << " ";
    	}
    	cout << endl;
    }



构造赋值

        set<int> s1;
    
    	s1.insert(10);
    	s1.insert(30);
    	s1.insert(20);
    	s1.insert(40);
    	printSet(s1);
    
    	//拷贝构造
    	set<int>s2(s1);
    	printSet(s2);
    
    	//赋值
    	set<int>s3;
    	s3 = s2;
    	printSet(s3);

- set容器插入数据时用insert
- 赋值用“=”
- set容器插入数据的数据会自动排序



大小交换

    	if (s1.empty())
    	{
    		cout << "s1为空" << endl;
    	}
    	else
    	{
    		cout << "s1不为空" << endl;
    		cout << "s1的大小为： " << s1.size() << endl;
    	}
    
        s1.swap(s2);

- 统计大小   --- size
- 判断是否为空   --- empty
- 交换容器   --- swap



插入删除

    	set<int> s1;
    	//插入
    	s1.insert(10);
    	s1.insert(30);
    	s1.insert(20);
    	s1.insert(40);
    	printSet(s1);
    
    	//删除
    	s1.erase(s1.begin());   //删除10，最小的
    	printSet(s1);
    
    	s1.erase(30);
    	printSet(s1);
    
    	//清空
    	//s1.erase(s1.begin(), s1.end());
    	s1.clear();
    	printSet(s1);

- 插入   --- insert
- 删除   --- erase
- 清空   --- clear



查找统计

        set<int> s1;
    	//插入
    	s1.insert(10);
    	s1.insert(30);
    	s1.insert(20);
    	s1.insert(40);
    	
    	//查找
    	set<int>::iterator pos = s1.find(30);   //返回迭代器
    
    	if (pos != s1.end())    //没有的话返回end
    	{
    		cout << "找到了元素 ： " << *pos << endl;
    	}
    	else
    	{
    		cout << "未找到元素" << endl;
    	}
    
    	//统计
    	int num = s1.count(30);
    	cout << "num = " << num << endl;

- 查找   ---  find    （返回的是迭代器）
- 统计   ---  count  （对于set，结果为0或者1）



对于set而言，find和count一个作用



set容器排序

默认从小到大

利用仿函数，自定义排序规则



内置数据类型

        set<int> s1;
    	s1.insert(10);
    	s1.insert(40);
    	s1.insert(20);
    	s1.insert(30);
    	s1.insert(50);
    
    	//默认从小到大
    	for (set<int>::iterator it = s1.begin(); it != s1.end(); it++) {
    		cout << *it << " ";
    	}
    	cout << endl;
    
    	//指定排序规则
    	set<int,MyCompare> s2;   //在创建的时候就规定好
    	s2.insert(10);
    	s2.insert(40);
    	s2.insert(20);
    	s2.insert(30);
    	s2.insert(50);
    
    	for (set<int, MyCompare>::iterator it = s2.begin(); it != s2.end(); it++) {
    		cout << *it << " ";
    	}
    	cout << endl;

    class MyCompare    //仿函数
    {
    public:
    	bool operator()(int v1, int v2) {   //重载小括号
    		return v1 > v2;    //从大到小
    	}
    };



自定义数组类型

    class Person
    {
    public:
    	Person(string name, int age)
    	{
    		this->m_Name = name;
    		this->m_Age = age;
    	}
    
    	string m_Name;
    	int m_Age;
    
    };
    
        set<Person, comparePerson> s;
    
    	Person p1("刘备", 23);
    	Person p2("关羽", 27);
    	Person p3("张飞", 25);
    	Person p4("赵云", 21);
    
    	s.insert(p1);
    	s.insert(p2);
    	s.insert(p3);
    	s.insert(p4);
    
    	for (set<Person, comparePerson>::iterator it = s.begin(); it != s.end(); it++)
    	{
    		cout << "姓名： " << it->m_Name << " 年龄： " << it->m_Age << endl;
    	}

    class comparePerson
    {
    public:
    	bool operator()(const Person& p1, const Person &p2)
    	{
    		//按照年龄进行排序  降序
    		return p1.m_Age > p2.m_Age;
    	}
    };

对于自定义数据类型，set必须指定排序规则才可以插入数据



2.8map容器：键值对

成对出现

- map中所有元素都是pair
- pair中第一个元素为key（键值），起到索引作用，第二个元素为value（实值）
- 所有元素都会根据元素的键值自动排序
  

- map不允许容器中有重复key值元素
- multimap允许容器中有重复key值元素



打印函数

    void printMap(map<int,int>&m)
    {
    	for (map<int, int>::iterator it = m.begin(); it != m.end(); it++)
    	{
    		cout << "key = " << it->first << " value = " << it->second << endl;
    	}
    	cout << endl;
    }

it->first，it->second



构造和赋值

        map<int,int>m; //默认构造
    	m.insert(pair<int, int>(1, 10));
    	m.insert(pair<int, int>(2, 20));
    	m.insert(pair<int, int>(3, 30));
    	printMap(m);
    
    	map<int, int>m2(m); //拷贝构造
    	printMap(m2);
    
    	map<int, int>m3;
    	m3 = m2; //赋值
    	printMap(m3);

    map<int,int>m; 
	m.insert(pair<int, int>(1, 10));



大小交换

        map<int, int>m;
    	m.insert(pair<int, int>(1, 10));
    	m.insert(pair<int, int>(2, 20));
    	m.insert(pair<int, int>(3, 30));
    
    	if (m.empty())
    	{
    		cout << "m为空" << endl;
    	}
    	else
    	{
    		cout << "m不为空" << endl;
    		cout << "m的大小为： " << m.size() << endl;
    	}
    	
    	map<int, int>m;
    	m.insert(pair<int, int>(1, 10));
    	m.insert(pair<int, int>(2, 20));
    	m.insert(pair<int, int>(3, 30));
    
    	map<int, int>m2;
    	m2.insert(pair<int, int>(4, 100));
    	m2.insert(pair<int, int>(5, 200));
    	m2.insert(pair<int, int>(6, 300));
    
    	cout << "交换前" << endl;
    	printMap(m);
    	printMap(m2);
    
    	cout << "交换后" << endl;
    	m.swap(m2);
    	printMap(m);
    	printMap(m2);

- 统计大小   --- size
- 判断是否为空   --- empty
- 交换容器   --- swap



插入删除

        //插入
    	map<int, int> m;
    	m.insert(pair<int, int>(1, 10));
    	printMap(m);
    
    	//删除
    	m.erase(m.begin());
    	printMap(m);
    
    	m.erase(3);
    	printMap(m);
    
    	//清空
    	m.erase(m.begin(),m.end());
    	m.clear();
    	printMap(m);

- 插入   --- insert 
- 删除   --- erase
- 清空   --- clear



查找统计

        map<int, int>m; 
    	m.insert(pair<int, int>(1, 10));
    	m.insert(pair<int, int>(2, 20));
    	m.insert(pair<int, int>(3, 30));
    
    	//查找
    	map<int, int>::iterator pos = m.find(3);
    
    	if (pos != m.end())
    	{
    		cout << "找到了元素 key = " << (*pos).first << " value = " << (*pos).second << endl;
    	}
    	else
    	{
    		cout << "未找到元素" << endl;
    	}
    
    	//统计
    	int num = m.count(3);
    	cout << "num = " << num << endl;

- 查找   ---  find    （返回的是迭代器）
- 统计   ---  count  （对于map，结果为0或者1）



map容器排序

        //默认从小到大排序
    	//利用仿函数实现从大到小排序
    	map<int, int, MyCompare> m;  //按key值从大到小
    
    	m.insert(make_pair(1, 10));
    	m.insert(make_pair(2, 20));
    	m.insert(make_pair(3, 30));
    	m.insert(make_pair(4, 40));
    	m.insert(make_pair(5, 50));
    
    	for (map<int, int, MyCompare>::iterator it = m.begin(); it != m.end(); it++) {
    		cout << "key:" << it->first << " value:" << it->second << endl;
    	}

    class MyCompare {
    public:
    	bool operator()(int v1, int v2) {
    		return v1 > v2;
    	}
    };

- 利用仿函数可以指定map容器的排序规则
- 对于自定义数据类型，map必须要指定排序规则,同set容器



三、STL算法



包含头文件#include<algorithm> 



3.1 遍历算法

- for_each     //遍历容器
- transform   //搬运容器到另一个容器中
  

for_each：遍历

        vector<int> v;
    	for (int i = 0; i < 10; i++) 
    	{
    		v.push_back(i);
    	}
    
    	//遍历算法
    	for_each(v.begin(), v.end(), print01);   //普通函数放 函数名
    	cout << endl;
    
    	for_each(v.begin(), v.end(), print02());  //仿函数放 函数名 +（）
    	cout << endl;  

    //普通函数
    void print01(int val) 
    {
    	cout << val << " ";
    }
    
    //函数对象
    class print02 
    {
     public:
    	void operator()(int val) 
    	{
    		cout << val << " ";
    	}
    };

for_each在实际开发中是最常用遍历算法，需要熟练掌握：

for_each(v.begin(), v.end(), print01);

void print01(int val) {cout << val << " ";}



transform：搬运

        vector<int>v;
    	for (int i = 0; i < 10; i++)
    	{
    		v.push_back(i);
    	}
    
    	vector<int>vTarget; //目标容器
    
    	vTarget.resize(v.size()); // 目标容器需要提前开辟空间
    
    	transform(v.begin(), v.end(), vTarget.begin(), TransForm());
    
    	for_each(vTarget.begin(), vTarget.end(), MyPrint());

    class TransForm
    {
    public:
    	int operator()(int val)
    	{
    		return val;
    	}
    };
    
    class MyPrint
    {
    public:
    	void operator()(int val)
    	{
    		cout << val << " ";
    	}
    };

搬运的目标容器必须要提前开辟空间，否则无法正常搬运



3.2 查找算法

- find                     //查找元素
- find_if               //按条件查找元素
- adjacent_find    //查找相邻重复元素
- binary_search    //二分查找法
- count                   //统计元素个数
- count_if             //按条件统计元素个数



find：查值

找 “=”，返回迭代器

        vector<int> v;
    	for (int i = 0; i < 10; i++) {
    		v.push_back(i + 1);
    	}
    
    	//查找容器中是否有 5 这个元素
    	vector<int>::iterator it = find(v.begin(), v.end(), 5);
    	if (it == v.end()) 
    	{
    		cout << "没有找到!" << endl;
    	}
    	else 
    	{
    		cout << "找到:" << *it << endl;
    	}
    
        vector<Person> v;
    
    	//创建数据
    	Person p1("aaa", 10);
    	Person p2("bbb", 20);
    	Person p3("ccc", 30);
    	Person p4("ddd", 40);
    
    	v.push_back(p1);
    	v.push_back(p2);
    	v.push_back(p3);
    	v.push_back(p4);
    
    	vector<Person>::iterator it = find(v.begin(), v.end(), p2);
    	if (it == v.end())   //重载==
    	{
    		cout << "没有找到!" << endl;
    	}
    	else 
    	{
    		cout << "找到姓名:" << it->m_Name << " 年龄: " << it->m_Age << endl;
    	}
    
    class Person {
    public:
    	Person(string name, int age) 
    	{
    		this->m_Name = name;
    		this->m_Age = age;
    	}
    	//重载==
    	bool operator==(const Person& p) 
    	{
    		if (this->m_Name == p.m_Name && this->m_Age == p.m_Age) 
    		{
    			return true;
    		}
    		return false;
    	}
    
    public:
    	string m_Name;
    	int m_Age;
    };

利用find可以在容器中找指定的元素，返回值是迭代器



find_if：查条件

找 “<,>,!=“，返回迭代器

    //内置数据类型
    class GreaterFive
    {
    public:
    	bool operator()(int val)
    	{
    		return val > 5;
    	}
    };
        vector<int> v;
    	for (int i = 0; i < 10; i++) {
    		v.push_back(i + 1);
    	}
    
    	vector<int>::iterator it = find_if(v.begin(), v.end(), GreaterFive());
    	if (it == v.end()) {
    		cout << "没有找到!" << endl;
    	}
    	else {
    		cout << "找到大于5的数字:" << *it << endl;
    	}
    
    
    //自定义数据类型
    class Person {
    public:
    	Person(string name, int age)
    	{
    		this->m_Name = name;
    		this->m_Age = age;
    	}
    public:
    	string m_Name;
    	int m_Age;
    };
    class Greater20
    {
    public:
    	bool operator()(Person &p)
    	{
    		return p.m_Age > 20;
    	}
    };
        vector<Person> v;
    	//创建数据
    	Person p1("aaa", 10);
    	Person p2("bbb", 20);
    	Person p3("ccc", 30);
    	Person p4("ddd", 40);
    
    	v.push_back(p1);
    	v.push_back(p2);
    	v.push_back(p3);
    	v.push_back(p4);
    
    	vector<Person>::iterator it = find_if(v.begin(), v.end(), Greater20());
    	if (it == v.end())
    	{
    		cout << "没有找到!" << endl;
    	}
    	else
    	{
    		cout << "找到姓名:" << it->m_Name << " 年龄: " << it->m_Age << endl;
    	}

find_if按条件查找使查找更加灵活，提供的仿函数可以改变不同的策略



adjacent_find：查相邻相同值

查找相邻重复元素

        vector<int> v;
    	v.push_back(1);
    	v.push_back(2);
    	v.push_back(5);
    	v.push_back(2);
    	v.push_back(4);
    	v.push_back(4);
    	v.push_back(3);
    
    	//查找相邻重复元素
    	vector<int>::iterator it = adjacent_find(v.begin(), v.end());
    	if (it == v.end()) {
    		cout << "找不到!" << endl;
    	}
    	else {
    		cout << "找到相邻重复元素为:" << *it << endl;
    	}

面试题中如果出现查找相邻重复元素，记得用STL中的adjacent_find算法



binary_search：二分查找

查找指定元素是否存在

查找指定的元素，查到 返回true  否则false

        vector<int>v;
    
    	for (int i = 0; i < 10; i++)
    	{
    		v.push_back(i);
    	}
    	//底层使用二分查找
    	bool ret = binary_search(v.begin(), v.end(),2);
    	if (ret)
    	{
    		cout << "找到了" << endl;
    	}
    	else
    	{
    		cout << "未找到" << endl;

二分查找法查找效率很高，值得注意的是查找的容器中元素必须的有序序列



count：数值

找 ”=“

        vector<int> v;
    	v.push_back(1);
    	v.push_back(2);
    	v.push_back(4);
    	v.push_back(5);
    	v.push_back(3);
    	v.push_back(4);
    	v.push_back(4);
    
    	int num = count(v.begin(), v.end(), 4);
    
    	cout << "4的个数为： " << num << endl;
    
    class Person
    {
    public:
    	Person(string name, int age)
    	{
    		this->m_Name = name;
    		this->m_Age = age;
    	}
    	bool operator==(const Person & p)  //重载==，年龄相等即可
    	{
    		if (this->m_Age == p.m_Age)
    		{
    			return true;
    		}
    		else
    		{
    			return false;
    		}
    	}
    	string m_Name;
    	int m_Age;
    };
        vector<Person> v;
    
    	Person p1("刘备", 35);
    	Person p2("关羽", 35);
    	Person p3("张飞", 35);
    	Person p4("赵云", 30);
    	Person p5("曹操", 25);
    
    	v.push_back(p1);
    	v.push_back(p2);
    	v.push_back(p3);
    	v.push_back(p4);
    	v.push_back(p5);
        
        Person p("诸葛亮",35);
    
    	int num = count(v.begin(), v.end(), p);
    	cout << "num = " << num << endl;

 统计自定义数据类型时候，需要配合重载 operator==



count_if：数条件

按条件统计

    class Greater4
    {
    public:
    	bool operator()(int val)
    	{
    		return val >= 4;
    	}
    };
        vector<int> v;
    	v.push_back(1);
    	v.push_back(2);
    	v.push_back(4);
    	v.push_back(5);
    	v.push_back(3);
    	v.push_back(4);
    	v.push_back(4);
    
    	int num = count_if(v.begin(), v.end(), Greater4());
    
    	cout << "大于4的个数为： " << num << endl;
    
    
    class Person
    {
    public:
    	Person(string name, int age)
    	{
    		this->m_Name = name;
    		this->m_Age = age;
    	}
    
    	string m_Name;
    	int m_Age;
    };
    class AgeLess35
    {
    public:
    	bool operator()(const Person &p)
    	{
    		return p.m_Age < 35;
    	}
    };
        vector<Person> v;
    
    	Person p1("刘备", 35);
    	Person p2("关羽", 35);
    	Person p3("张飞", 35);
    	Person p4("赵云", 30);
    	Person p5("曹操", 25);
    
    	v.push_back(p1);
    	v.push_back(p2);
    	v.push_back(p3);
    	v.push_back(p4);
    	v.push_back(p5);
    
    	int num = count_if(v.begin(), v.end(), AgeLess35());
    	cout << "小于35岁的个数：" << num << endl;

按值统计用count，按条件统计用count_if



3.3 排序算法

- sort             //对容器内元素进行排序
- random_shuffle   //洗牌   指定范围内的元素随机调整次序
- merge           // 容器元素合并，并存储到另一容器中
- reverse       // 反转指定范围的元素



sort：排序

    void myPrint(int val)
    {
    	cout << val << " ";
    }
        vector<int> v;
    	v.push_back(10);
    	v.push_back(30);
    	v.push_back(50);
    	v.push_back(20);
    	v.push_back(40);
    
    	//sort默认从小到大排序
    	sort(v.begin(), v.end());
    	for_each(v.begin(), v.end(), myPrint);
    	cout << endl;
    
    	//从大到小排序
    	sort(v.begin(), v.end(), greater<int>());//系统提供greater<int>()
    	for_each(v.begin(), v.end(), myPrint);
    	cout << endl;

sort属于开发中最常用的算法之一

sort(v.begin(), v.end());

sort(v.begin(), v.end(), greater<int>());



random_shuffle：洗牌

洗牌   指定范围内的元素随机调整次序

    class myPrint
    {
    public:
    	void operator()(int val)
    	{
    		cout << val << " ";
    	}
    };
        
        srand((unsigned int)time(NULL));  //使每次不一样
    	vector<int> v;
    	for(int i = 0 ; i < 10;i++)
    	{
    		v.push_back(i);
    	}
    	for_each(v.begin(), v.end(), myPrint());
    	cout << endl;
    
    	//打乱顺序
    	random_shuffle(v.begin(), v.end());
    	for_each(v.begin(), v.end(), myPrint());
    	cout << endl;



merge：合并

两个容器元素合并，并存储到另一容器中

两个容器必须是有序的

    class myPrint
    {
    public:
    	void operator()(int val)
    	{
    		cout << val << " ";
    	}
    };
    
        vector<int> v1;
    	vector<int> v2;
    	for (int i = 0; i < 10 ; i++) 
        {
    		v1.push_back(i);
    		v2.push_back(i + 1);
    	}
    
    	vector<int> vtarget;
    	//目标容器需要提前开辟空间
    	vtarget.resize(v1.size() + v2.size());
    	//合并  需要两个有序序列
    	merge(v1.begin(), v1.end(), v2.begin(), v2.end(), vtarget.begin());
    	for_each(vtarget.begin(), vtarget.end(), myPrint());
    	cout << endl;

vtarget.resize(v1.size() + v2.size());

两个序列必须是有序的



reverse：反转

将容器内元素进行反转

    class myPrint
    {
    public:
    	void operator()(int val)
    	{
    		cout << val << " ";
    	}
    };
        vector<int> v;
    	v.push_back(10);
    	v.push_back(30);
    	v.push_back(50);
    	v.push_back(20);
    	v.push_back(40);
    
    	cout << "反转前： " << endl;
    	for_each(v.begin(), v.end(), myPrint());
    	cout << endl;
    
    	cout << "反转后： " << endl;
    
    	reverse(v.begin(), v.end());
    	for_each(v.begin(), v.end(), myPrint());
    	cout << endl;



3.4 拷贝和替换算法

- copy                      // 容器内指定范围的元素拷贝到另一容器中
- replace                // 将容器内指定范围的旧元素修改为新元素
- replace_if          // 容器内指定范围满足条件的元素替换为新元素
- swap                     // 互换两个容器的元素



copy：拷贝

        vector<int> v1;
    	for (int i = 0; i < 10; i++) {
    		v1.push_back(i + 1);
    	}
    	vector<int> v2;
    	v2.resize(v1.size());   //手动开空间
    
    	copy(v1.begin(), v1.end(), v2.begin());
    
    	for_each(v2.begin(), v2.end(), myPrint());
    	cout << endl;

利用copy算法在拷贝时，目标容器记得提前开辟空间



replace：值替换

将容器内指定范围的旧元素修改为新元素（值）

        vector<int> v;
    	v.push_back(20);
    	v.push_back(30);
    	v.push_back(20);
    	v.push_back(40);
    	v.push_back(50);
    	v.push_back(10);
    	v.push_back(20);
    
    	cout << "替换前：" << endl;
    	for_each(v.begin(), v.end(), myPrint());
    	cout << endl;
    
    	//将容器中的20 替换成 2000
    	cout << "替换后：" << endl;
    	replace(v.begin(), v.end(), 20,2000);
    
    	for_each(v.begin(), v.end(), myPrint());
    	cout << endl;

replace会替换区间内满足条件的元素



replace_if：条件替换

将区间内满足条件的元素，替换成指定元素（条件）

    class ReplaceGreater30
    {
    public:
    	bool operator()(int val)
    	{
    		return val >= 30;
    	}
    };
        vector<int> v;
    	v.push_back(20);
    	v.push_back(30);
    	v.push_back(20);
    	v.push_back(40);
    	v.push_back(50);
    	v.push_back(10);
    	v.push_back(20);
    
    	cout << "替换前：" << endl;
    	for_each(v.begin(), v.end(), myPrint());
    	cout << endl;
    
    	//将容器中大于等于的30 替换成 3000
    	cout << "替换后：" << endl;
    	replace_if(v.begin(), v.end(), ReplaceGreater30(), 3000);
    
    	for_each(v.begin(), v.end(), myPrint());
    	cout << endl;

replace_if按条件查找，可以利用仿函数灵活筛选满足的条件



swap：交换

        vector<int> v1;
    	vector<int> v2;
    	for (int i = 0; i < 10; i++) {
    		v1.push_back(i);
    		v2.push_back(i+100);
    	}
    
    	cout << "交换前： " << endl;
    	for_each(v1.begin(), v1.end(), myPrint());
    	cout << endl;
    	for_each(v2.begin(), v2.end(), myPrint());
    	cout << endl;
    
    	cout << "交换后： " << endl;
    	swap(v1, v2);
    
    	for_each(v1.begin(), v1.end(), myPrint());
    	cout << endl;
    	for_each(v2.begin(), v2.end(), myPrint());
    	cout << endl;



3.5 算术生成算法

算术生成算法属于小型算法，使用时包含的头文件为 #include <numeric>

- accumulate      // 计算容器元素累计总和
- fill                 // 向容器中添加元素



accumulate：求和

计算区间内 容器元素累计总和

        vector<int> v;
    	for (int i = 0; i <= 100; i++) {
    		v.push_back(i);
    	}
    
    	int total = accumulate(v.begin(), v.end(), 0);  //0是起始值
    
    	cout << "total = " << total << endl;

accumulate使用时头文件注意是 numeric，这个算法很实用



fill：填充

向容器中填充指定的元素

        vector<int> v;
    	v.resize(10);
    	//填充
    	fill(v.begin(), v.end(), 100);
    
    	for_each(v.begin(), v.end(), myPrint());
    	cout << endl;

利用fill可以将容器区间内元素填充为 指定的值



3.6 常用集合算法

- set_intersection          // 求两个容器的交集
- set_union                       // 求两个容器的并集
- set_difference              // 求两个容器的差集



set_intersection：交集

求交集，两个集合必须是有序序列

        vector<int> v1;
    	vector<int> v2;
    	for (int i = 0; i < 10; i++)
        {
    		v1.push_back(i);
    		v2.push_back(i+5);
    	}
    
    	vector<int> vTarget;
    	//取两个里面较小的值给目标容器开辟空间
    	vTarget.resize(min(v1.size(), v2.size()));
    
    	//返回目标容器的最后一个元素的迭代器地址
    	vector<int>::iterator itEnd = 
            set_intersection(v1.begin(), v1.end(), v2.begin(), v2.end(), vTarget.begin());
    
    	for_each(vTarget.begin(), itEnd, myPrint());
    	cout << endl;

- 求交集的两个集合必须的有序序列
- 目标容器开辟空间需要从两个容器中取小值   
  vTarget.resize(min(v1.size(), v2.size()));
- set_intersection返回值既是交集中最后一个元素的位置



set_union：并集

求并集，两个集合必须是有序序列

        vector<int> v1;
    	vector<int> v2;
    	for (int i = 0; i < 10; i++) {
    		v1.push_back(i);
    		v2.push_back(i+5);
    	}
    
    	vector<int> vTarget;
    	//取两个容器的和给目标容器开辟空间
    	vTarget.resize(v1.size() + v2.size());
    
    	//返回目标容器的最后一个元素的迭代器地址
    	vector<int>::iterator itEnd = 
            set_union(v1.begin(), v1.end(), v2.begin(), v2.end(), vTarget.begin());
    
    	for_each(vTarget.begin(), itEnd, myPrint());
    	cout << endl;

- 求并集的两个集合必须的有序序列
- 目标容器开辟空间需要两个容器相加    
  vTarget.resize(v1.size() + v2.size());
- set_union返回值既是并集中最后一个元素的位置



set_difference：差集

求差集，两个集合必须是有序序列

        vector<int> v1;
    	vector<int> v2;
    	for (int i = 0; i < 10; i++) {
    		v1.push_back(i);
    		v2.push_back(i+5);
    	}
    
    	vector<int> vTarget;
    	//取两个里面较大的值给目标容器开辟空间
    	vTarget.resize( max(v1.size() , v2.size()));
    
    	//返回目标容器的最后一个元素的迭代器地址
    	cout << "v1与v2的差集为： " << endl;
    	vector<int>::iterator itEnd = 
            set_difference(v1.begin(), v1.end(), v2.begin(), v2.end(), vTarget.begin());
    	for_each(vTarget.begin(), itEnd, myPrint());
    	cout << endl;
    
    
    	cout << "v2与v1的差集为： " << endl;
    	itEnd = set_difference(v2.begin(), v2.end(), v1.begin(), v1.end(), vTarget.begin());
    	for_each(vTarget.begin(), itEnd, myPrint());
    	cout << endl;

- 求差集的两个集合必须的有序序列
- 目标容器开辟空间需要从两个容器取较大值
  vTarget.resize( max(v1.size() , v2.size()));
- set_difference返回值既是差集中最后一个元素的位置
