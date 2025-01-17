##### the vitual base class

```
class ClxBase
{
public:
    ClxBase() {};
    virtual ~ClxBase() {};

    virtual void DoSomething() { cout << "Do something in class ClxBase!" << endl; };
};

class ClxDerived : public ClxBase
{
public:
    ClxDerived() {};
    ~ClxDerived() { cout << "Output from the destructor of class ClxDerived!" << endl; }; 

    void DoSomething() { cout << "Do something in class ClxDerived!" << endl; };
};

ClxBase *pTest = new ClxDerived;
pTest->DoSomething();
delete pTest;

OUT:
  Do something in class ClxDerived!
  Output from the destructor of class ClxDerived!

  但是，如果把类ClxBase析构函数前的virtual去掉，那输出结果就是下面的样子了：
  Do something in class ClxDerived!
  
  也就是说，类ClxDerived的析构函数根本没有被调用！
  一般情况下类的析构函数里面都是释放内存资源，而析构函数不被调用的话就会造成内存泄漏。
  我想所有的C++程序员都知道这样的危险性。当然，如果在析构函数中做了其他工作的话，那你的所有努力也都是白费力气。
  所以，文章开头的那个问题的答案就是
      －－这样做是为了当用一个基类的指针删除一个派生类的对象时，派生类的析构函数会被调用。
      当然，并不是要把所有类的析构函数都写成虚函数。因为当类里面有虚函数的时候，编译器会给类添加一个虚函数表，里面来存放虚函数指针，
      这样就会增加类的存储空间。所以，只有当一个类被用来作为基类的时候，才把析构函数写成虚函数。
```
