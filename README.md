# CPP-LinkedList
Simple and efficient linked list data structure

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
    int value;
public:
    void Run(Test* test);
    void Run2(const LinkedList<Test>& list) {
    	list.Iterate(this, [](UserClass* _this,Test* test) {
		test->data += _this->value;
	});
    }
};

```

```cpp
// initialize like this
LinkedList<Test> linkedList =  LinkedList<Test>();
// or you can initialize like this
LinkedList<Test> linkedList = LinkedList<Test>({new Test(1), new Test(2), new Test(2) });
// add elements like this
linkedList.AddFront(new TestChild(1));
linkedList.AddFront(new Test(2));
linkedList.AddFront(new Test(3));
linkedList.AddBack(new Test(0));
linkedList.AddBack(new Test(-1));
// reach elements like this
TestChild* testChild = linkedList[0];
testChild = linkedList.FindNodeByType<TestChild>();
// remove elements like this
linkedList.Remove(testChild);
delete linkedList.RemoveFront(); 
Test* removed = linkedList.RemoveBack();

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
// easier way for classes
linkedList.IterateClass<UserClass>(
{ 
    userClass, [](UserClass* userClass, Test* test)
    {
        userClass->Run(test);
    }
});
```
