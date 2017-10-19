## Go 语言函数
- 函数是基本的代码块，用于执行一个任务。
- Go 语言最少有个 main() 函数。
- 你可以通过函数来划分不同功能，逻辑上每个函数执行的是指定的任务。
- 函数声明告诉了编译器函数的名称，返回类型，和参数。
- Go 语言标准库提供了多种可动用的内置的函数。例如，len() 函数可以接受不同类型参数并返回该类型的长度。如果我们传入的是字符串则返回字符串的长度，如果传入的是数组，则返回数组中包含的函数个数。
#### 1.函数定义
Go 语言函数定义格式如下：
```
func function_name( [parameter list] ) [return_types] {
   函数体
}
```
#### 2.函数定义解析：
- func：函数由 func 开始声明
- function_name：函数名称，函数名和参数列表一起构成了函数签名。
 -parameter list：参数列表，参数就像一个占位符，当函数被调用时，你可以将值传递给参数，这个值被称为实际参数。参数列表指定的是参数类型、顺序、及参数个数。参数是可选的，也就是说函数也可以不包含参数。
- return_types：返回类型，函数返回一列值。return_types 是该列值的数据类型。有些功能不需要返回值，这种情况下 return_types 不是必须的。
- 函数体：函数定义的代码集合。
#### 3.实例
以下实例为 max() 函数的代码，该函数传入两个整型参数 num1 和 num2，并返回这两个参数的最大值：
```
/* 函数返回两个数的最大值 */
func max(num1, num2 int) int {
   /* 声明局部变量 */
   var result int

   if (num1 > num2) {
      result = num1
   } else {
      result = num2
   }
   return result 
}
```
函数调用
当创建函数时，你定义了函数需要做什么，通过调用改函数来执行指定任务。
调用函数，向函数传递参数，并返回值，例如：
```
package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var a int = 100
   var b int = 200
   var ret int

   /* 调用函数并返回最大值 */
   ret = max(a, b)

   fmt.Printf( "最大值是 : %d\n", ret )
}

/* 函数返回两个数的最大值 */
func max(num1, num2 int) int {
   /* 定义局部变量 */
   var result int

   if (num1 > num2) {
      result = num1
   } else {
      result = num2
   }
   return result 
}
```
以上实例在 main() 函数中调用 max（）函数，执行结果为：
```
最大值是 : 200
```
函数返回多个值
Go 函数可以返回多个值，例如：
```
package main

import "fmt"

func swap(x, y string) (string, string) {
   return y, x
}

func main() {
   a, b := swap("Mahesh", "Kumar")
   fmt.Println(a, b)
}
```
以上实例执行结果为：
```
Kumar Mahesh
```
#### 4.函数参数
- 函数如果使用参数，该变量可称为函数的形参。
形参就像定义在函数体内的局部变量。
调用函数，可以通过两种方式来传递参数：


|传递类型|描述
|---|---
|值传递|值传递是指在调用函数时将实际参数复制一份传递到函数中，这样在函数中如果对参数进行修改，将不会影响到实际参数
|引用传递|引用传递是指在调用函数时将实际参数的地址传递到函数中，那么在函数中对参数所进行的修改，将影响到实际参数。

**默认情况下，Go 语言使用的是值传递，即在调用过程中不会影响到实际参数.**

#### 5.Go 语言函数值传递值
Go 函数
- 传递是指在调用函数时将实际参数复制一份传递到函数中，这样在函数中如果对参数进行修改，将不会影响到实际参数。
默认情况下，Go 语言使用的是值传递，即在调用过程中不会影响到实际参数。
以下定义了 swap() 函数：
```
/* 定义相互交换值的函数 */
func swap(x, y int) int {
   var temp int

   temp = x /* 保存 x 的值 */
   x = y    /* 将 y 值赋给 x */
   y = temp /* 将 temp 值赋给 y*/

   return temp;
}
```
接下来，让我们使用值传递来调用 swap() 函数：
```
package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var a int = 100
   var b int = 200

   fmt.Printf("交换前 a 的值为 : %d\n", a )
   fmt.Printf("交换前 b 的值为 : %d\n", b )

   /* 通过调用函数来交换值 */
   swap(a, b)

   fmt.Printf("交换后 a 的值 : %d\n", a )
   fmt.Printf("交换后 b 的值 : %d\n", b )
}

/* 定义相互交换值的函数 */
func swap(x, y int) int {
   var temp int

   temp = x /* 保存 x 的值 */
   x = y    /* 将 y 值赋给 x */
   y = temp /* 将 temp 值赋给 y*/

   return temp;
}
```
以下代码执行结果为：
```
交换前 a 的值为 : 100
交换前 b 的值为 : 200
交换后 a 的值 : 100
交换后 b 的值 : 200
```
**程序中使用的是值传递, 所以两个值并没有实现交互，我们可以使用 引用传递** 来实现交换效果。

#### 6.Go 语言函数引用传递值
Go 函数
- 引用传递是指在调用函数时将实际参数的地址传递到函数中，那么在函数中对参数所进行的修改，将影响到实际参数。
引用传递指针参数传递到函数内，以下是交换函数 swap() 使用了引用传递：
```
/* 定义交换值函数*/
func swap(x *int, y *int) {
   var temp int
   temp = *x    /* 保持 x 地址上的值 */
   *x = *y      /* 将 y 值赋给 x */
   *y = temp    /* 将 temp 值赋给 y */
}
```
以下我们通过使用引用传递来调用 swap() 函数：
```
package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var a int = 100
   var b int= 200

   fmt.Printf("交换前，a 的值 : %d\n", a )
   fmt.Printf("交换前，b 的值 : %d\n", b )

   /* 调用 swap() 函数
   * &a 指向 a 指针，a 变量的地址
   * &b 指向 b 指针，b 变量的地址
   */
   swap(&a, &b)

   fmt.Printf("交换后，a 的值 : %d\n", a )
   fmt.Printf("交换后，b 的值 : %d\n", b )
}

func swap(x *int, y *int) {
   var temp int
   temp = *x    /* 保存 x 地址上的值 */
   *x = *y      /* 将 y 值赋给 x */
   *y = temp    /* 将 temp 值赋给 y */
}
```
以上代码执行结果为：
```
交换前，a 的值 : 100
交换前，b 的值 : 200
交换后，a 的值 : 200
交换后，b 的值 : 100
```

#### 7.函数用法
|函数用法|描述
|---|---
|函数作为值|函数定义后可作为值来使用
|闭包|闭包是匿名函数，可在动态编程中使用
|方法|方法就是一个包含了接受者的函数.

#### 8.Go 语言函数作为值
- Go 语言可以很灵活的创建函数，并作为值使用。以下实例中我们在定义的函数中初始化一个变量，该函数仅仅是为了使用内置函数 math.sqrt() ，实例为：
```
package main

import (
   "fmt"
   "math"
)

func main(){
   /* 声明函数变量 */
   getSquareRoot := func(x float64) float64 {
      return math.Sqrt(x)
   }

   /* 使用函数 */
   fmt.Println(getSquareRoot(9))

}
```
以上代码执行结果为：
```
3
```
#### 9.Go 语言函数闭包
- Go 语言支持匿名函数，可作为闭包。匿名函数是一个"内联"语句或表达式。匿名函数的优越性在于可以直接使用函数内的变量，不必申明。
以下实例中，我们创建了函数 getSequence() ，返回另外一个函数。该函数的目的是在闭包中递增 i 变量，代码如下：
```
package main

import "fmt"

func getSequence() func() int {
   i:=0
   return func() int {
      i+=1
     return i  
   }
}

func main(){
   /* nextNumber 为一个函数，函数 i 为 0 */
   nextNumber := getSequence()  

   /* 调用 nextNumber 函数，i 变量自增 1 并返回 */
   fmt.Println(nextNumber())
   fmt.Println(nextNumber())
   fmt.Println(nextNumber())
   
   /* 创建新的函数 nextNumber1，并查看结果 */
   nextNumber1 := getSequence()  
   fmt.Println(nextNumber1())
   fmt.Println(nextNumber1())
}
```
以上代码执行结果为：
```
1
2
3
1
2
```

#### 10.Go 语言函数方法

- Go 语言中同时有函数和方法。一个方法就是一个包含了接受者的函数，接受者可以是命名类型或者结构体类型的一个值或者是一个指针。所有给定类型的方法属于该类型的方法集。语法格式如下：
```
func (variable_name variable_data_type) function_name() [return_type]{
   /* 函数体*/
}
```
下面定义一个结构体类型和该类型的一个方法：
```
package main

import (
   "fmt"  
)

/* 定义函数 */
type Circle struct {
  radius float64
}

func main() {
  var c1 Circle
  c1.radius = 10.00
  fmt.Println("Area of Circle(c1) = ", c1.getArea())
}

//该 method 属于 Circle 类型对象中的方法
func (c Circle) getArea() float64 {
  //c.radius 即为 Circle 类型对象中的属性
  return 3.14 * c.radius * c.radius
}
```
以上代码执行结果为：
```
Area of Circle(c1) =  314
```

