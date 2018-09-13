封装
继承
多态
类：
class ClassName {
    //属性声明
    //方法声明
}
class Employee {
    private $name;
    private $title;
    protected $wage;

    protected function clockIn() {
        echo "Member $this=>name clocked in at ".date("h:i:s");
    }

    protected function clockOut() {
        echo "Member $this->name clocked out at ".date("h:i:s");
    }

    function __set($propName, $propValue) {
        echo "Nonexistent variable:\$$propName";
    }

}
对象： 类的实例
$employee = new Employee();
##属性
###1.声明属性
###2.属性作用域
public: 
private:子类和实例化的对象直接访问
portected： 只有在类中才能访问，子类也可以访问和操作这些属性
final：之内不能覆盖这个属性 
static;

__set()和__get();
##常量


