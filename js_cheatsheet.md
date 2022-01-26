# Javascript ES6

### Variables

> Switch variables 

    var a = "3"
    var b = "8"

    function switchVariables() {
        var c = a
        a = b
        b = c
    }


### Functions

> BMI Calculator

    function bmiCalculator(w, h) {
    var bmi = w / Math.pow(h, 2)
       return bmi
    }
    var bmi = bmiCalculator(65, 1.8)
    console.log(bmi)

### If-Statements

> Fibonacci Generator

    var bmi = bmiCalculator(65, 1.8)
    console.log(bmi)

    function fibonacciGenerator(n) {
        var output = []
        if(n === 1) {
            output = [0]
        } else if (n === 2) {
            output = [0, 1]
        } else {
            output = [0, 1]
            for (let i = 2; i < n; i++) {
            output.push(output[output.length -1] + output[output.length-2])
            }
        }
        return output
    }
    var fibonacciSequenz = fibonacciGenerator(20)
    console.log(fibonacciSequenz)

### Map Function

> Create a new array by doing something with each item in an array. Map expects a function as an arguement.

    var numbers = [1, 34, 65, 77]
    var doubleNumbers = numbers.map((x) => {
        return x*2
    });

> Or shorter

    var numbers = [1, 34, 65, 77]
    var doubleNumbers = numbers.map(x => x*2);

### Filter Function
> Create a new array by keeping the items that return true.

    var numbers = [1, 34, 65, 77]
    var evenNumbers = numbers.filter( function (num) {
        return num % 2 === 0
    })

> or shorter 

    var numbers = [1, 34, 65, 77]
    var evenNumber = number.filter(num => num % 2 === 0)

### Reduce Function 

> Accumulate a value by doing something to each item in an array.

    var numbers = [1, 34, 65, 77]
    var sum = numbers.reduce( function(accumulator, currentNumber) {
        return accumulator + currentNumber
    })

> or shorter

     var numbers = [1, 34, 65, 77]
     var sum = numbers.reduce((accumulator, currentNumber) => accumulator + currentNumber )

### Find Function

> Find - find the first item that matches from an array.

    var numbers = [1, 34, 65, 77]
    var newNumber = numbers.find( function(num) {
        return num > 10
    })

> or shorter

    var numbers = [1, 34, 65, 77]
    var newNumber = numbers.find( num => num > 10)


### FindIndex Function

    var numbers = [1, 34, 65, 77]
    var index = numbers.findIndex( num => num > 10)
