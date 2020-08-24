# Swift 5.3

1. 变量总是在使用前初始化好
2. 数组索引会有越界错误检查
3. 整数会被检查是否溢出
4. 可选性确保nil值被显示处理
5. 内存被自动管理
6. 错误处理允许从意外故障中进行受控恢复

## 简单的值
1.使用let来定义一个常量
2.使用var来定义一个变量
```swift
var myVariable = 42
myVariable = 50
let myConstant = 42
```

3. 常量和变量必须复制给他相应的类型，但是你没必要在声明时显示指出类型
```swift
1> let implicitInteger = 70
implicitInteger: Int = 70
2> let implicitDouble = 70.0
implicitDouble: Double = 70
3> let expliciDouble: Double = 70
expliciDouble: Double = 70
```

4. 值永远不会配隐式转换为另一个类型，如果你需要转换一个值成另一个不同的类型，那就显示地实例一个期望的类型  
```swift
let label = "The width is"
let width = 94
let widthLabel = label + String(width)
```

5. 有个更简单的方式在字符串中包含值，用()将值包括，并且在开始括号(前写个反斜线\，例如:
```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```

6. 使用三个双引号 """ 包括的字符串可以跨多行，类似Python
```swift
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
"""
```

## 数组和字典
1. 创建数组和字典使用中括号[]包含，使用索引和键来访问元素，可以允许在最后一个元素后面多加一个逗号。
```swift
var shoppingList = ["catfish", "water", "tulips"]
shoppingList[1] = "bottle of water"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations"
```
2. 数组会随着你添加元素而自动增长
```swift
shoppingList.append("blue paint")
print(shoppingList)
```
3. 创建一个空的数组或者字典，使用初始化语法
```swift
let emptyArray = [String]()
let emptyDictionary = [String: Float]()
```
4. 如果类型信息可以被推断，你可以用[]创建一个空数组，用[:]创建一个空字典
```swift
shoppingList = []
occupations = [:]
```

### 控制流
1. 使用if和switch进行条件判断，使用for-in，while，repeat-while进行循环。
圆括号包裹条件变量或循环变量是可选的，而大括号包含语句体是必须的。
```swift
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
print(teamScore)
```
2. 在一个if语句中，条件必须是一个布尔表达式，这意味着类似 if score {...}这样的代码是个错误，因为不会进行隐式地与零进行比较。
```swift
if 2 {
    print("Hello")
}
error: repl.swift:38:4: error: cannot convert value of type 'Int' to expected condition type 'Bool'
if 2 {
```
3. 你可以将if和let一起使用来处理可能是丢失的值，他们的值表示为是可选的一个可选的值可以包含值也可以包含nil来表示这个值是丢失的。写一个问号在值的类型后面来标记这个值是可选的。
```swift
var optionalString: String? = "Hello"
print(optionalString == nil)

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```
如果可选的值是nil，那么if let条件判断会是false，大括号中的代码会被跳过。否则可选值会被解包并赋值给let后面的常量，这让解包后的值在{}代码块中可以使用。

4. 另一种方式处理可选值，使用 ?? 运算符提供一个默认值，如果可选值丢失（即值为nil），那么默认值将会被使用。
```swift
let nickname: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickname ?? fullName)"
```
5. switch 支持很多数据类型和各种各样的比较运算，他们不局限于整数和相等性测试。
```swift
let vegetable = "red pepper"
switch vegetable {
    case "celery":
        print("Add some raisins and make ants on a log")
    case "cucumber", "watercress":
        print("That would make a good tea sandwich.")
    case let x where x.hasSuffix("pepper"):
        print("Is it a spicy \(x)?")
    default:
        print("Everything tastes good in soup.")
}
```
在执行完匹配到的case代码后，程序就从switch语句中推出，执行不会继续到下一个case，所以没有必要显示地在每个case语句后见写break来推出switch语句。

6. 使用for-in根据键值对去迭代字典的每一项。字典是无序的集合，所以迭代它们的键值对时也是随机顺序的。
```swift
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
var largeKind = "Prime"
for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
            largeKind = kind
        }
    }
}
print(largest)
print(largeKind)
```

7. 使用while去重复代码块知道条件发生变化。repeat-while语句循环条件放在最后，确保循环至少可以执行一次。
```swift
var n = 2
while n < 100 {
    n *= 2
}
print(n)

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
```
8. 你可以通过使用 ..< 制作一个索引范围，这样就可以在循环中使用索引
```swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
```
使用 ..< 让范围忽略上界， 使用 .. 让范围包含上下界。

### 函数和闭包
1. 使用func声明一个函数。把参数列表放在圆括号()中一起添加在函数名字后面来调用该函数。使用 -> 分隔函数名字和函数范围类型。
```swift
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```
2. 使用一个元组生成一个复合值，例如：让一个函数返回多个值，一个元组的元素既可以通过名字访问也可以通过数字来访问。
```swift
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
let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
print(statistics.sum)
print(statistics.2)
```
3. 函数可以嵌套定义，嵌套的函数可以访问外层函数中的变量。在一个比较大和复杂的函数中，你可以使用嵌套定义函数来组织你的代码，使之更明朗易读。
```swift
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```
4. 函数是第一类型值，这意味着一个函数可以将另一个函数作为值来返回。
```swift
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```
5. 一个函数可以将另一个函数作为它的参数来传入。
```swift
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
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
6. 函数其实是闭包的一种特殊情况：代码块可以之后被调用。闭包中的代码可以访问在创建闭包的作用域中可用的变量和函数，即使在执行闭包时闭包位于不同的范围内， 您已经看到了一个嵌套函数的例子。你可以使用{}包裹代码来创建一个匿名闭包，使用in从代码中分离参数和返回类型。
```swift
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
numbers.map({ (number: Int) -> Int in
    if number % 2 != 0 {
        return 0
    } else {
        return number
    }
})
```
7. 你可以使用数字来引用参数， 这个方法在很短的闭包中非常有用。作为函数的最后一个参数传递的闭包参数可以紧跟在圆括号的后面。如果闭包是一个函数的唯一参数时，你可以完全省略圆括号。
```swift
var numbers = [20, 19, 7, 12]
let sortedNumbers = numbers.sorted { $0 > $1}
print(sortedNumbers)
numbers.sorted() { $0 > $1}
numbers.sorted(by: > )
```

### 对象和类
1. 使用class后接类的名字来创建一个类。在类中声明属性和常量变量的定义是一样的方式，只是它在类的环境中，同样，方法和函数的声明是同样的方式。
```swift
class Shape {
    var numberOfSides = 0

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```
2. 通过在类型放一个()来创建一个类的实例，使用点语法访问属性和方法。
```swift
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```
3. 上面的Shape一些重要的东西：当实例被创建时，初始化器设置类。使用init去创建一个。
```swift
class NamedShape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
        self.name = name
    }

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
var rect = NamedShape(name: "Rectangle")
```
self是用来区分属性name和参数name的。
使用deinit创建一个去初始化器，如果你需要在对象退出内存之前执行一些清理工作

4. 子类在类名之后包含他们的父类的名字, 用冒号：分隔。没有要求一个类一定要作为任何标准根类的子类，因此可以根据需要包含或者省略父类。
```swift
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() -> Double {
        return sideLength * sideLength
    }

    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)"
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()

class Circle: NamedShape {
    let PI = 3.14
    var radius: Double

    init(radius: Double, name: String) {
        self.radius = radius
        super.init(name: name)
        numberOfSides = 0
    }

    func area() -> Double {
        return PI * radius * radius
    }

    override func simpleDescription() -> String {
        return "A circle with radius \(radius)"
    }
}
```
用override标记子类中的方法要重写父类的方法实现。意外的重写父类方法而不写override标记，这回引发编译错误。

5. 除了简单存储属性外，属性还可以有getter和setter方法。
```swift
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }

    var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }

    override func simpleDescription() -> String {
        return "An equialteral triangle with sides of length \(sideLength)"
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
triangle.perimeter = 9.9
print(triangle.sideLength)
```
在perimeter的setter中，新的值有一个隐式的名字newValue。你可以提供一个显示的名字在set后面的圆括号()中。
Notice: EquialateralTriangle类中的初始化器有三个不同的步骤：
1. 设置子类中声明的属性的值
2. 调用父类的初始化器
3. 改变定义在父类中的属性的值。任何使用方法，getters或者setters等附加设置工作都可以在此时完成。

6. 如果你不需要计算属性，但是仍想要提供代码运行在设置新值之前或者之后。使用willSet和didSet。当值在初始化器外发生任何更改时，都会运行您提供的代码。下面的代码保证三角形的边长总是和四边形的边长一样的。
```swift
class TriangleAndSquare {
    var triangle: EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
    }

    var square: Square {
        willSet {
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
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength)
```
7. 类和可选值一起使用的时候，你可以在方法，属性和subscripting之前写 ?。如果在 ? 之前的值是nil，那么 ? 之后的一切都会被忽略，并且整个表达式的值是nil。否则，可选值会被解包，并且在?之后的一切作用于解包的值。在这两种情况中，整个表达式的值是一个可选值。
```swift
let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
let sideLength = optionalSquare?.sideLength
```

### 枚举和结构
1. 使用enum创建一个枚举。就像类和其他命名的类型一样，枚举可以定义方法关联他们。
```swift
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine,ten
    case jack, queen, king

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
let aceRawValue = ace.rawValue
```
默认情况下，Swift把原始值从0开始赋值，并且之后每个增长1。但是你把ace显示的赋值为1，并且接下来的原始值都会以1为基础顺序增1赋值。你也可以使用字符串或者浮点数作为一个枚举的原始类型。使用rawValue属性访问枚举的原始值。

2. 使用init?(rawValue:) 初始化器根据一个原始值去生成一个枚举实例。它要么返回对应的枚举类型的原始值，要么就返回nil，如果没匹配上的话。
```swift
if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}
```



