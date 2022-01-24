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

