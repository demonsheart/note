### Swift基础

#### 变量与常量

```swift
var myVariable = 42
let myConstant = 42
```

#### 类型自动获取与声明

```swift
// 自动获取
let implicitInteger = 70
let implicitDouble = 70.0
// 声明
let explicitDouble: Double = 70
```

#### swift不会隐式转换 类型转换必须显示转换

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```

#### nil值

Swift 的 `nil` 和 Objective-C 中的 `nil` 并不一样。在 Objective-C 中，`nil` 是一个指向不存在对象的指针。在 Swift 中，`nil` 不是指针——它是一个确定的值，用来表示值缺失。任何类型的可选状态都可以被设置为 `nil`，不只是对象类型。

#### 可用\\()来解析成字符串

```swift
let num = 3
let apples = "I have \(num) apples." //  I have 3 apples.
```

#### 多行字符串可以用"""

```swift
let sentences = """
I love you.
You love me too.
"""
```

#### 数组和字典

```swift
var shoppingList = ["catfish", "water", "tulips"]
shoppingList[1] = "bottle of water"
shoppingList.append("blue paint")

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
 ]
occupations["Jayne"] = "Public Relations"

// 空字典和数组
let emptyArray = [String]()
let emptyDic = [String: Float]()

// 如果类型可推测 可简化写法 array as []  dictionary as [:]
shoppingList = []
occupations = [:]
```

#### for-in

```swift
let scores = [55, 66, 77, 88]
var totalScore = 0
for score in scores{
  totalScore += score
}
print(totalScore)
```

#### 可选类型与if

```swift
var optionalString: String? = "Hello"
print(optionalString == nil)

var optionalName: String? = nil
var greeting = "Hello!"
if let name = optionalName {// 值缺失 不会进入花括号
    greeting = "Hello, \(name)"
    print(greeting)
}
```

#### ??

通过使用 `??` 操作符来提供一个默认值。如果可选值缺失的话，可以使用默认值来代替。

```swift
let nickName: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickName ?? fullName)" // Hi John Appleseed
```

#### switch

`switch` 支持任意类型的数据以及各种比较操作——不仅仅是整数以及测试相等。

```swift
let vegetable = "red pepper"
switch vegetable {
case "celery":
    print("Add some raisins and make ants on a log.")
case "cucumber", "watercress":
    print("That would make a good tea sandwich.")
case let x where x.hasSuffix("pepper"):
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}
```

#### 遍历字典

```swift
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)
```

#### ..<表示下标范围

```swift
var total = 0
for i in 0..<4 {
  total += i
}
print(total) // 6
```

#### 函数

```swift
func greet(person: String, day: String) -> String {
  return "Hello \(person), today is \(day)"
}
greet(person: "Bob", day: "Thursday")

// _表示不使用参数标签
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")

// 多返回值
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0

    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }

    return (min, max, sum)
}
let statistics = calculateStatistics(scores:[5, 3, 100, 3, 9])
print(statistics.sum)
print(statistics.2)

// 函数可嵌套 被嵌套函数可以访问外侧变量
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5 // 可访问外侧变量
    }
    add()
    return y
}
returnFifteen()


// 函数作为返回值
func makeIncrementer() -> ((Int) -> Int) {
  func addOne(number: Int) -> Int {
    return 1 + number
  }
  return addOne;
}
var increment = makeIncrementer()
increment(7)


// 函数作为参数
func hasAnyMatches(list: [Int], condition: (int) -> Bool) -> Bool {
  for item in list {
    if condition(item) {
      return true
    }
  }
  return false
}
func lessThanTen(number: Int) -> Bool {
  return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)
```

#### 可变参数

一个*可变参数（variadic parameter）*可以接受零个或多个值。函数调用时，你可以用可变参数来指定函数参数可以被传入不确定数量的输入值。通过在变量类型名后面加入（`...`）的方式来定义可变参数。

可变参数的传入值在函数体中变为此类型的一个数组。例如，一个叫做 `numbers` 的 `Double...` 型可变参数，在函数体内可以当做一个叫 `numbers` 的 `[Double]` 型的数组常量。

下面的这个函数用来计算一组任意长度数字的 *算术平均数（arithmetic mean)*：



```swift
func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
arithmeticMean(1, 2, 3, 4, 5)
// 返回 3.0, 是这 5 个数的平均数。
arithmeticMean(3, 8.25, 18.75)
// 返回 10.0, 是这 3 个数的平均数。
```

#### 输入输出参数

函数参数默认是常量。试图在函数体中更改参数值将会导致编译错误。这意味着你不能错误地更改参数值。如果你想要一个函数可以修改参数的值，并且想要在这些修改在函数调用结束后仍然存在，那么就应该把这个参数定义为*输入输出参数（In-Out Parameters）*。

定义一个输入输出参数时，在参数定义前加 `inout` 关键字。一个 `输入输出参数`有传入函数的值，这个值被函数修改，然后被传出函数，替换原来的值。

你只能传递变量给输入输出参数。你不能传入常量或者字面量，因为这些量是不能被修改的。当传入的参数作为输入输出参数时，需要在参数名前加 `&` 符，表示这个值可以被函数修改。

> 注意
>
> 输入输出参数不能有默认值，而且可变参数不能用 `inout` 标记。

下例中，`swapTwoInts(_:_:)` 函数有两个分别叫做 `a` 和 `b` 的输入输出参数：

```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

`swapTwoInts(_:_:)` 函数简单地交换 `a` 与 `b` 的值。该函数先将 `a` 的值存到一个临时常量 `temporaryA` 中，然后将 `b` 的值赋给 `a`，最后将 `temporaryA` 赋值给 `b`。

你可以用两个 `Int` 型的变量来调用 `swapTwoInts(_:_:)`。需要注意的是，`someInt` 和 `anotherInt` 在传入 `swapTwoInts(_:_:)` 函数前，都加了 `&` 的前缀：

```swift
var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
print("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// 打印“someInt is now 107, and anotherInt is now 3”
```

从上面这个例子中，我们可以看到 `someInt` 和 `anotherInt` 的原始值在 `swapTwoInts(_:_:)` 函数中被修改，尽管它们的定义在函数体外。

#### 闭包

可以使用 `{}` 来创建一个匿名闭包。使用 `in` 将参数和返回值类型的声明与闭包函数体进行分离。

```swift
var numbers = [20, 19, 7, 12]
numbers.map({
  (number: Int) -> Int in
  let result = 3 * number
  return result
})

// 如果一个闭包的类型已知，比如作为一个代理的回调，你可以忽略参数，返回值，甚至两个都忽略。单个语句闭包会把它语句的值当做结果返回。
let mappedNumbers = numbers.map({ number in 3 * number})

// 你可以通过参数位置而不是参数名字来引用参数——这个方法在非常短的闭包中非常有用。
// 当一个闭包作为最后一个参数传给一个函数的时候，它可以直接跟在圆括号后面。
// 当一个闭包是传给函数的唯一参数，你可以完全忽略圆括号。
let sortedNumbers = numbers.sorted{ $0 > $1 }
```

#### 对象和类

结构体有默认的逐一构造器，而类没有

```swift
class NamedShape {
  var numberOfSizes: Int = 0
  var name: String
  
  init(name: String) { // 构造函数
    self.name = name
  }
  deinit() { // 析构函数
    // code
  }
  func simpleDescription() -> String {
    return "A shape with \(numberOfSides) sides."
  }
}

// 继承
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() ->  Double {
        return sideLength * sideLength
    }
		// 重写方法必须有 override关键字
    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```

#### 类成员的计算属性

```swift
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }
	  // set get 计算属性
    var perimeter: Double {
        get {
             return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }

    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter) // 调用get
triangle.perimeter = 9.9  // 调用set
print(triangle.sideLength)
```

#### willSet & didSet

需要在设置一个新值之前或者之后运行代码，使用 `willSet` 和 `didSet`。写入的代码会在属性值发生改变时调用，但不包含构造器中发生值改变的情况。

```swift
class TriangleAndSquare {
    // 保证三角形和正方形边长一致
    var triangle: EquilateralTriangle {
        willSet { // 当三角形边长发生改变 改变正方形的边长
            square.sideLength = newValue.sideLength
        }
    }
    var square: Square {
        willSet { // 当正方形边长发生改变 改变三角形的边长
            triangle.sideLength = newValue.sideLength
        }
    }
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}
var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
print(triangleAndSquare.square.sideLength)
print(triangleAndSquare.triangle.sideLength)
triangleAndSquare.square = Square(sideLength: 50, name: "larger square") // 值发生改变 触发WillSet函数
print(triangleAndSquare.triangle.sideLength)
```

#### 处理可选值

处理变量的可选值时，你可以在操作（比如方法、属性和子脚本）之前加 `?`。如果 `?` 之前的值是 `nil`，`?` 后面的东西都会被忽略，并且整个表达式返回 `nil`。否则，可选值会被解包，之后的所有代码都会按照解包后的值运行。在这两种情况下，整个表达式的值也是一个可选值。

```swift
var optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
var sideLength = optionalSquare?.sideLength // 2.5

optionalSquare = nil
sideLength = optionalSquare?.sideLength // nil
```

#### 枚举和结构体

```swift
// 默认情况下，Swift 按照从 0 开始每次加 1 的方式为原始值进行赋值
enum Rank: Int { // Rank: Int 表示有原始值
    case ace = 1 // Ace 被显式赋值为 1
    // 剩下的原始值会按照顺序赋值。
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king
    
    // 函数 由枚举成员调用
    func simpleDescription() -> String {
        switch self {
            case .ace:
                return "ace"
            case .jack:
                return "jack"
            case .queen:
                return "queen"
            case .king:
                return "king"
            default:
                return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue // .rawValue取值
print(Rank.two.rawValue) // 2
print(Rank.king.rawValue) // 13
print(Rank.ace.simpleDescription()) // 由枚举成员调用

// 使用 init?(rawValue:) 初始化构造器来从原始值创建一个枚举实例。如果存在与原始值相应的枚举成员就返回该枚举成员，否则就返回 nil。
if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}

// 无原始值
enum Suit {
    case spades, hearts, diamonds, clubs
    func simpleDescription() -> String {
        switch self {
        case .spades:
            return "spades"
        case .hearts:
            return "hearts"
        case .diamonds:
            return "diamonds"
        case .clubs:
            return "clubs"
        }
    }
}
let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()


// 如果枚举成员的实例有原始值，那么这些值是在声明的时候就已经决定了，这意味着不同枚举实例的枚举成员总会有一个相同的原始值。当然我们也可以为枚举成员设定关联值，关联值是在创建实例时决定的。这意味着同一枚举成员不同实例的关联值可以不相同
enum ServerResponse {
    case result(String, String)
    case failure(String)
    case null(String)
}
// 枚举实例 设定关联值
let success = ServerResponse.result("6:00 am", "8:09 pm")
let failure = ServerResponse.failure("Out of cheese.")
let null = ServerResponse.null("null")

// 关联值的获取问题

switch null { // success failure null 都是SeverResponse的实例 
              // 在 switch 里，枚举成员使用缩写 .hearts 来引用
    case let .result(sunrise, sunset):
        print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
    case let .failure(message):
        print("Failure...  \(message)")
    case let .null(mess):
        print(mess)
}


// 使用 struct 来创建一个结构体。结构体和类有很多相同的地方，包括方法和构造器。它们之间最大的一个区别就是结构体是传值，类是传引用。
struct Card {
    var rank: Rank
    var suit: Suit
    func simpleDescription() -> String {
        return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
      // The 3 of spades
    }
}
let threeOfSpades = Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription()
```

#### 值类型 & 引用类型

> ***值类型***是这样一种类型，当它被赋值给一个变量、常量或者被传递给一个函数的时候，其**值会被*拷贝*。**
>
> 在之前的章节中，你已经大量使用了值类型。实际上，Swift 中所有的基本类型：整数（integer）、浮点数（floating-point number）、布尔值（boolean）、字符串（string)、数组（array）和字典（dictionary），都是值类型，其底层也是使用结构体实现的。
>
> Swift 中所有的结构体和枚举类型都是值类型。这意味着它们的实例，以及实例中所包含的任何值类型的属性，在代码中传递的时候都会被复制。

>与值类型不同，*引用类型*在被赋予到一个变量、常量或者被传递到一个函数时，其值不会被拷贝。因此，**使用的是已存在实例的引用，而不是其拷贝**。

#### 恒等运算符

判定两个常量或者变量是否引用同一个类实例有时很有用。

* 相同 ===
* 不相同 !==

请注意，“相同”（用三个等号表示，`===`）与“等于”（用两个等号表示，`==`）的不同。“相同”表示两个类类型（class type）的常量或者变量引用同一个类实例。“等于”表示两个实例的值“相等”或“等价”，判定时要遵照设计者定义的评判标准。



#### AnyObject & Any

> AnyObject：可以代表任何class类型的实例；
> Any：可以代表任何类型，甚至包括方法(func)类型。

#### 协议和拓展

协议可以理解为接口(抽象类)

```swift
protocol SomeProtocol {
    // 这里是协议的定义部分
    // 可以是属性、方法、构造器等等
}
struct SomeStructure: FirstProtocol, AnotherProtocol {
    // 这里是结构体的定义部分
}
class SomeClass: SomeSuperClass, FirstProtocol, AnotherProtocol {
    // 这里是类的定义部分
}
```

##### 属性要求

如果协议要求属性是可读可写的，那么该属性不能是常量属性或只读的计算型属性。如果协议只要求属性是可读的，那么该属性不仅可以是可读的，如果代码需要的话，还可以是可写的。

协议总是用 `var` 关键字来声明变量属性，在类型声明后加上 `{ set get }` 来表示属性是*可读可写*的，*可读*属性则用 `{ get }` 来表示：

```swift
protocol SomeProtocol {
    var mustBeSettable: Int { get set }
    var doesNotNeedToBeSettable: Int { get }
}
```

##### 方法要求

**不支持为协议中的方法提供默认参数**

##### 异变方法要求

如果你在协议中定义了一个实例方法，该方法会**改变遵循该协议的类型的实例**，那么在定义协议时需要在方法前加 **`mutating`** 关键字。这使得结构体和枚举能够遵循此协议并满足此方法要求。

> 注意
>
> 实现协议中的 `mutating` 方法时，若是类类型，则不用写 `mutating` 关键字。而对于结构体和枚举，则必须写 `mutating` 关键字。

##### 类专属的协议

你通过添加 `AnyObject` 关键字到协议的继承列表，就可以限制协议只能被类类型采纳（以及非结构体或者非枚举的类型）。

```swift
protocol SomeClassOnlyProtocol: AnyObject, SomeInheritedProtocol {
    // 这里是类专属协议的定义部分
}
```

在以上例子中，协议 `SomeClassOnlyProtocol` 只能被类类型采纳。如果尝试让结构体或枚举类型采纳 `SomeClassOnlyProtocol`，则会导致编译时错误。

##### 检查协议的一致性

你可以使用 [类型转换]() 中描述的 `is` 和 `as` 操作符来检查协议一致性，即是否遵循某协议，并且可以转换到指定的协议类型。检查和转换协议的语法与检查和转换类型是完全一样的：

- `is` 用来检查实例是否遵循某个协议，若遵循则返回 `true`，否则返回 `false`；
- `as?` 返回一个可选值，当实例遵循某个协议时，返回类型为协议类型的可选值，否则返回 `nil`；
- `as!` 将实例强制向下转换到某个协议类型，如果强转失败，将触发运行时错误

```swift
let objects: [AnyObject] = [
    Circle(radius: 2.0), // 遵守HasArea
    Country(area: 243_610), // 遵守HasArea
    Animal(legs: 4) // 不遵守HasArea
]
for object in objects {
    if let objectWithArea = object as? HasArea {
        print("Area is \(objectWithArea.area)")
    } else {
        print("Something that doesn't have an area")
    }
}
// Area is 12.5663708
// Area is 243610.0
// Something that doesn't have an areas
```

##### 为协议扩展添加限制条件

```swift
extension Collection where Element: Equatable {
    func allEqual() -> Bool {
        for element in self {
            if element != self.first {
                return false
            }
        }
        return true
    }
}
```

#### 泛型

##### 泛型函数

```swift
func swap<T>(_ a: inout T, _ b: inout T) {
  	let tmp = a
  	a = b
  	b = tmp
}
```

##### 类型约束

在一个类型参数名后面放置一个类名或者协议名，并用冒号进行分隔，来定义类型约束。下面将展示泛型函数约束的基本语法（与泛型类型的语法相同）：



```swift
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
    // 这里是泛型函数的函数体部分
}
```

上面这个函数有两个类型参数。第一个类型参数 `T` 必须是 `SomeClass` 子类；第二个类型参数 `U` 必须符合 `SomeProtocol` 协议。

