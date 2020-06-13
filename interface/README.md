# Interface in GO Lang 


## The Basics

The interface is a powerful tool in GO Lang that helps the language to bring polymorphism functinalities (not exactly but somehow close )
Using Interfaces we can represent single value in multiple types.

Structs in GO Lang implements object type behavior (objects in Javascript) and Struct methods can be closely related to method-function of an object (in Js world)

#### Object in Javascript

What things you need to install the software and how to install them
```
var car1 = {
 	Model: "Fiat 500"
  	Color : "white"
	fullDetails : function() {
    	return this.Model + " of color " + this.Color;
  	}
};
console.log( car1.fullDetails() )
```

#### Struct in Go

What things you need to install the software and how to install them
```
type car struct {
    Model string
    Color string
}
func (c car) fullDetails() string {
    return  c.Model  + " of color " + c.Color
}


func main() {
    
    car1:= car{
        Model: "Fiat 500"
        Color: "white"
    }
    fmt.Println(car1.fullDetails())    
}
```

A type may have single or multiple methods. what those methods will do( means what operations will take place inside that method function) is defined by the type.


**An interface is just a collection method signatures**  ( method name and return type ). so an Interface only cares about method name and return type. the interface does not care what those methods will do ( what operations will take place inside that method function ). **The interface contains only the signatures of the methods, but not their implementation** (means interface never declares the behavior but it defines the behavior of the object )

<br>

> When all the methods of a TYPE are available inside an INTERFACE, it is said the TYPE implements that INTERFACE

<br>



###### Example basic struct and interface in go
```
type Employee struct {  
    empId    int
    salary int
    bonus    int
}
func (e Employee) TotalSalary() int {  
    return p.salary + p.bonus
}
```
In this example ***Employee*** is a struct type and ***TotalSalary*** is a method of ***Employee*** struct.
what this ***TotalSalary*** will do or perform is defined by this ***Employee*** struct.

```
type SalaryCalculator interface {  
    TotalSalary() int
}
```
In this example ***SalaryCalculator*** is an interface. it has a method ***TotalSalary***  and the return type ***int***.  what this method ***TotalSalary*** will do or perform is not the concern of this interface. it only checks if any type ( like struct, int, etc) implement this ***TotalSalary()*** and return type ***int***,  will automatically  implement this interface ***SalaryCalculator***



<br>
<br>
<br>


## Interface : Static and Dynamic type


```
type item interface {
    Area() float64
    Volume() float64
}
func main() {
    var i item
    fmt.Printf("value of i :  %v and type of i: %T", i ,i)
}
```

here we specify an interface **item** and i is an instance of that interface.when we print value and type of variable **i**, the result is : value of i : < nil > and type of i : < nil >

<br>
<br>

> #### Dynamic Value :
>
> let's understand this: the value is: nil because an interface does not have ***static value***,  rather it points to a ***dynamic value***. the dynamic value is the value of another type (like a struct variable ) that implements the interface.


<br>

> #### Dynamic and Static Type :
>
> An Interface variable has 2 types.
>
> - **static type**: the interface itself (in this case **item** )
> - **Dynamic type / Concrete type**:  type of the variable (like a variable of a struct type ) which implements the interface

<br>



here in this implement, no other type implements the interface, so the value is nil, and the dynamic type is also nil. when we print the type of an interface, it returns the dynamic type and its static type remains hidden.


<br>
<br>

```
type Box struct {
    L, W, H float64
}
func (b Box) Area() float64 {
    return  2*( b.H * b.W) + 2*(b.H * b.L) + 2*(b.W * b.L)
}
func (b Box) Volume() float64 {
    return b.L * b.W  * b.H 
}


type item interface {
    Area() float64
    Volume() float64
}

func main() {
    var i item
    i = Box {2,3,4}
    fmt.Printf("value of i :  %v and type of i: %T", i ,i)
    fmt.Println("")
    b1 := Box{2,3,4}
    fmt.Printf("value of b1 :  %v and type of b1: %T", b1 ,b1)
    fmt.Println("")
    fmt.Println("is 'i' and 'b1' are of the same value :", i==b1)
}
```

here Box struct has 2 methods : **Area()** & **Volume()** . and the interface **item** has method signatures of :  **Area()** & **Volume()**. so the **Box** struct type implements the **item** interface.

<br>

var **i** is an instance of interface **item** and as struct **Box** implements **item**, so we can directly assign **i** to an instance of **Box**.

<br>

>**item** implements **Box**
>**instance of item** Assign to  **instance of Box** ( **i** = **Box{2,3,4}**  )
> also type of **i** is **main.Box** 

<br>

another variable **b1** is a direct instance of **Box{2,3,4}**
```
fmt.Println("is 'i' and 'b1' are of the same value :", i==b1)
```
Now when we do a comparison between **i** and **b1** ( **i** instance of an interface  & **b1** instance of a struct ), we see their values are the same.

<br>




## dynamic type and value: why it is called dynamic


```
type Box struct {
    L, W, H float64
}
func (b Box) Area() float64 {
    return  2*( b.H * b.W) + 2*(b.H * b.L) + 2*(b.W * b.L)
}
func (b Box) Volume() float64 {
    return b.L * b.W  * b.H 
}


type Ball struct {
    R float64
}
func (b Ball) Area() float64 {
    return 4 * 3.14 * b.R * b.R
}
func (b Ball) Volume() float64 {
    return (4 / 3) * 3.14 * b.R * b.R * b.R
}

type item interface {
    Area() float64
    Volume() float64
}

func main() {
    var b1 = Box{5.0, 10.0, 8.0}
    fmt.Printf("Type = %T, Area = %v , Volume = %v \n", b1, b1.Area(), b1.Volume())

    var b2 = Ball{5.0}
    fmt.Printf("Type = %T, Area = %v , Volume = %v \n", b2, b2.Area(), b2.Volume())

    var i item
    fmt.Printf("value of i :  %v and type of i: %T   \n", i ,i)
    
    i = Box {2,3,4}
    fmt.Printf("value of i :  %v and type of i: %T   \n", i ,i)
    fmt.Println("is 'i' and 'b1' are of the same value :", i==b1)
	
    i = Ball{5.0}
 	fmt.Printf("value of i :  %v and type of i: %T   \n", i ,i)
    fmt.Println("is 'i' and 'b2' are of the same value :", i==b2)
}
```

<br>

in this example, the variable **i** instance of the interface **item**. item has 2 method signature: Area() & Volume(). now both **Box** and **Ball** struct have methods Area() & Volume(). so both **Box** and **Ball** struct implements interface **item**

<br>

the variable **i** is assigned to the **Box** struct value. so **i** become of => Type  **main.Box** ,( value of  Area = 52 , Volume = 24 ) 
then the variable **i** is assigned to the **Ball** struct value. so **i** become of => Type **main.Ball** ,( value of  Area = 314 , Volume = 392.5 )

In Go lang variables are static type, means variable types are explicitly declared and we can not their type  ( from int to float, or string to int, etc ). 

In this example, we can see, the type of variable **i** changes. first, the type of **i** was  **nil**, then it becomes the type of **main.Box**, then it becomes the type of **main.Ball**. we can say that an interface dynamically holds the reference to the underlying type-instance ( **value** and  **type** of that type-instance).

this phenomenon can only happen with an **instance of an interface**. the dynamic type of an interface means that it can hold a reference to different types (e.g. string, int, ...) and that it can change at runtime, whereas a static type is checked at compile-time and cannot change.


<br>
<br>








## Empty Interface


```
type CustomString string

type Box struct {
    L, W, H float64
}

func Details(i interface{}) {
    fmt.Printf("given element Type : %T and Value: %v \n", i, i)
}

func main() {
    c := CustomString("some string")
    b := Box{2,3,4}
    Details(c)
    Details(b)
}
```

<br>

we make a custom string type **CustomString** and a struct **Box**. **c** is an instance of **CustomString** and **b** is an instance of **Box**.

now the function **Details**  will take an **empty interface** . as an **empty interface** has **no methods** so it can be implemented by **any type**, so variable **b** and **c** is valid input for the function **Details**




## No of Interfaces a Type can implement

A type can implement any no of Interfaces

```
type Box struct {
    L, W, H float64
}
func (b Box) Area() float64 {
    return  2*( b.H * b.W) + 2*(b.H * b.L) + 2*(b.W * b.L)
}
func (b Box) Volume() float64 {
    return b.L * b.W  * b.H 
}

type AreaCalculator interface {
        Area() float64
 }
type VolumeCalculator interface {
        Volume() float64
}

func main() {
    
    b := Box{2,3,4}
    var a AreaCalculator =b
    var v VolumeCalculator = b
    
    fmt.Println("Area of a  is :" , a.Area())
    fmt.Printf("a => Type : %T and Value: %v \n", a, a)
    
    fmt.Println("Volume of v is :" , v.Volume())
    fmt.Printf("v => Type : %T and Value: %v \n", v, v)

}
```

**b** is an instance of struct"Box" and it has 2 methods **Area()** and **Volume()** . now we have 2 interfaces, interface **AreaCalculator** has only method signature **Area()** and interface **VolumeCalculator** has only method signature **Volume()**

in this case, variable"b" implements both interfaces **AreaCalculator** and **VolumeCalculator**. 
**a** is an instance of **AreaCalculator** and **v** is an instance of **VolumeCalculator**.

so we will get the result :
Area of a  is : 52
a => Type : main.Box and Value: {2 3 4} 
Volume of v is : 24
v => Type : main.Box and Value: {2 3 4}



<br>

## Meaning of static type for an Interface

now we can see that both **a** and **v** has the same type ( main.Box ) and value( {2 3 4} ) . but these 2 variables are not same .

we can put this code :
```
fmt.Println("is 'a' and 'v' are of the same value :", a==v)
```
result will be : 
invalid operation: a == v (mismatched types AreaCalculator and VolumeCalculator)

this is because these 2 variables **a** and **s** has the same dynamic Type and Value. but their Static Type is different  (AreaCalculator and VolumeCalculator ) so these 2 variables are not the same.


## Extract the dynamic value


```
type Box struct {
    L, W, H float64
}
func (b Box) Area() float64 {
    return  2*( b.H * b.W) + 2*(b.H * b.L) + 2*(b.W * b.L)
}
func (b Box) Volume() float64 {
    return b.L * b.W  * b.H 
}

type AreaCalculator interface {
        Area() float64
 }
type VolumeCalculator interface {
        Volume() float64
}

func main() {
    
    b := Box{2,3,4}
    var a AreaCalculator =b
    var v VolumeCalculator = b
    fmt.Println("Area of a  is :" , a.Volume())
    fmt.Println("Volume of v is :" , v.Area())
}
```
but if we try to use: a.Volume()  or  v.Area() it will show error :

> **The result :**
> a.Volume undefined (type AreaCalculator has no field or method Volume)
> v.Area undefined (type VolumeCalculator has no field or method Area)

because **a** is an instance of **AreaCalculator** which has only 1 method signature **Area()**, it does not have **Volume()** method. similarly **v** an instance of **VolumeCalculator** does have **Volume()** method but not the **Area()** method.


<br>

to make this work we have to extract the **Dynamic Value** of the struct implementing these Interface ( **Box** struct ).

```
type Box struct {
    L, W, H float64
}

func (b Box) Area() float64 {
    return  2*( b.H * b.W) + 2*(b.H * b.L) + 2*(b.W * b.L)
}

func (b Box) Volume() float64 {
    return b.L * b.W  * b.H 
}

type AreaCalculator interface {
    Area() float64
}

type VolumeCalculator interface {
    Volume() float64
}

func main() {
    
    b := Box{2,3,4}
    var a AreaCalculator =b
    var v VolumeCalculator = b
    
    a1 := a.(Box)
    v1 := v.(Box)

    fmt.Println("Area of a  is :" , a1.Volume())
    fmt.Println("Volume of v is :" , v1.Area())
    fmt.Println("is 'a1' and 'v1' are of the same value :", a1==v1)
}
```

we extract the struct **Box** from **a** by **a.(Box)** same for **v** by **v.(Box)**
the format is i. (Type) ... but **Type** must implement the interface **i** or this will be an error.

now **a1** become the **Box{2,3,4}** itself , same , **v1** become the **Box{2,3,4}** itself. so now **a1** and **v1** is identical in both by value and by dynamic and static type. so ( a1 == v1) is True


<br>

## Type assertion

**Type assertion** is a way to retrieve dynamic value from interface type value.


for type assertion, we need an **interface** and a **type** which implements that interface
<br>

> #### the expression is : v.(T) 
>
> - "v" is the interface 
> - "T" is the type 
>    - T can be an "interface"
>    - T can be any other type (int, string, etc)
>

<br>

### v.(T)  => T can be an "interface" 

for v.(T)  :  If T  is an interface type then such assertion checks if dynamic type of v implements interface T:

```
type I interface {
        walk() string
}
type J interface {
        quack() string
}
type K interface {
        bark() string
}
type S struct{
     name string
}

func (s S) walk() string{
    return  s.name+"can walk"
}
func (s S) quack() string{
    return s.name+"can quack"
}
func main() {
    var i I
    i = S{"bird"}
    fmt.Printf("Details => Type : %T and Value: %v \n", i, i)
    fmt.Printf("Details => Type : %T and Value: %v \n", i.(J) ,i.(J))
    fmt.Printf("Details => Type : %T and Value: %v \n", i.(K) ,i.(K))
}
```

as **S{"dog"}** has 2 methods: **walk** and **quack**. now interface **I** have **walk** method so **S** can implement **I**, same interface  **J**  have  **quack** method, so **S** can also implement **J** . but interface **K** have only **bark**  method so **S** can not implement **K**

**i.(J)**  => dynamic type of **i** ( which is **S** ) implements **J**, so it will have no issue

<br>

**i.(K)** => dynamic type of **iv** ( which is **S** ) does not implements **K**, so it will have error: 
( interface conversion: main.S is not main.K: missing method bark )

<br>

### v.(T)  => T can be any other type (int, string, etc)

for **v.(T)**  :  If **T**  is not an interface type then such assertion checks if dynamic type of **v** is identical to **T**

```
type I interface {
    walk() string
}

type A struct{
    name string
}
func (a A) walk() string{
    return  a.name+"can walk"
}
type B struct{
    name string
}
func (b B) walk() string{
    return  b.name+"can walk"
}

func main() {
    var i I
    i = A{"Bob"}
    fmt.Printf("Details => Type : %T and Value: %v \n", i.(A), i.(A))
    fmt.Printf("Details => Type : %T and Value: %v \n", i.(B), i.(B))
}
```

here **I** interface has method signature **walk()**. both struct **A** and **B** have **walk()** method, so both implements **I** interface

> **i.(A)** => dynamic type of **i** ( which is **A** ) is  identical to **A** , so it will work fine

> **i.(B)** => dynamic type of **i** ( which is **A** ) is not identical to **B** , so it will give an error ( although **B** implements **I**, but the variable **i** which  instance of **I**, has a dynamic value of **A**, that's why the issue is arising )


### some more example

```
func printValue(i interface{}) {
    fmt.Printf("The value of v is: %v", i.(int))
}

func main() {
    v := 10
    printValue(v)
}
```

this example will work fine. Because **v** is of type **int**, when **printValue** function take the argument  **i interface{}** => then **i** got dynamic value of **int** from **v** . so **i(int)** will work fine.


<br>

```
func printValue(i interface{}) {
    fmt.Printf("The value of v is: %v",  v.(string))
}

func main() {
    v := 10
    printValue(v)
}
```

this example will not work and give error . Because **v** is of type **int**, when **printValue** function take the argument  **i interface{}** => then **i** got dynamic value of **int** from **v** . so **i(string)** will not work as i have dynamic value of **int** not **string**.

<br>

```
func main() {
    var greeting interface{} = "5"
    greetingStr := greeting.(string)
    fmt.Printf("The value is: %v and type is : %T \n",  greetingStr , greetingStr)
    
    var greeting2 interface{} = 5
    greetingInt2 := greeting2.(int)
    fmt.Printf("The value is: %v and type is : %T \n",  greetingInt2 , greetingInt2)
    
    var greeting3 interface{} = "5"
    greetingStr3 := greeting3.(int)
    fmt.Printf("The value is: %v and type is : %T \n",  greetingStr3 , greetingStr3)
    
    var greeting4 interface{} = 5
    greetingInt4 := greeting4.(string)
    fmt.Printf("The value is: %v and type is : %T \n",  greetingInt4 , greetingInt4)
}
```

> first 2 blocks will run perfectly  because :
>	"v.(T)" is matching the criteria: dynamic type of v == T
> but the last 2 will not work because :
>	 "v.(T)" is not matching the criteria: dynamic type of v != T


<br>



## Interface : pointer vs value receiver


