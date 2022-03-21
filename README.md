# C-LinkedList
LinkedList

```cpp

class Test 
{
public:
	int data = 0;
	Test() { }
	Test(int _data) : data(_data) { }
	~Test() { }
    virtual int GetData() const { return data; };
};

class TestChild : public Test
{
public:
    TestChild() : Test() {  }
    TestChild(int _data) : Test(_data) { }
    ~TestChild() { }
    int GetData() const { return data; };
};

class UserClass
{
public:
    void Run(Test* test);
};

```

```cpp
LinkedList<Test> linkedList =  LinkedList<Test>();
auto testChild = new TestChild(2);
linkedList.AddFront(testChild);
linkedList.AddFront(new Test(1));
linkedList.AddFront(new Test(3));

linkedList.AddBack(new Test(4));

linkedList.Remove(testChild);
auto userClass = new UserClass();

linkedList.Iterate([](Test* test) {
    test->data += 10;
	std::cout << test->data << std::endl;
});

linkedList.IterateClass<UserClass>(
    LinkedList<Test>::ClassIterator<UserClass>(userClass, [](UserClass* userClass, Test* test)
    {
        userClass->Run(test);
    })
);

linkedList.IterateClass<UserClass>(
{ 
    userClass, [](UserClass* userClass, Test* test)
    {
        userClass->Run(test);
    }
});
```
