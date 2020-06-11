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


