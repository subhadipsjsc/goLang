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
>
>**instance of item** Assign to  **instance of Box**
>
>**i** = **Box{2,3,4}**  
>
> also type of **i** is **main.Box** 

<br>

another variable **b1** is a direct instance of **Box{2,3,4}**
```
    fmt.Println("is 'i' and 'b1' are of the same value :", i==b1)
```
Now when we do a comparison between **i** and **b1** ( **i** instance of an interface  & **b1** instance of a struct ), we see their values are the same.

<br>




### dynamic type and value: why it is called dynamic


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

