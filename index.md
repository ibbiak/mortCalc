---
title       : Monthly Amortizing Mortgage Payment Calculator
subtitle    : Developing Data Products, Data Science Specialization
author      : ibbi a k
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax, shiny, interactive, bootstrap]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
logo        : pi.jpg

---

## Shinny App
### Monthly Amortizing Mortgage Payment Calculator

The application takes the following inputs relating to the mortgage:

1. The value of the mortgage / loan amount
2. The interest rate for the mortgage
3. The term of the mortgage (in years)

and outputs the expected monthly mortgage payments for an amortizing mortgage.

The monthly mortgage payments are calculate as using the following formula:

$$P\frac{i\left(1 + i \right)^n}{\left(1 + i \right)^n - 1}$$

where P is the value of the mortgage, i is the annual interest rate divded by 12 and n is the term of the mortgage in months.

---

## Shinny App
### User Interface


```r
shinyUI(pageWithSidebar(
        headerPanel("Monthly Amortizing Mortgage Payment Calculator"),
        sidebarPanel(
                h6("Please enter the Mortgage Amount, Interest Rate and Term of the Mortgage in the input boxes provided below"),
                h6("The inputs will be used to calculate your monthly mortgage payments after you click the Submit button"),
                numericInput("Value", "Mortgage Amount", 0, min = 0),
                numericInput("rate", label = "Annual Interest Rate in %", 0, min =0),
                numericInput("Term", "Mortgage Term in Years", 0, min = 0),
                submitButton("Submit")
                ),
        mainPanel(
                h3("Monthly Mortgage Payment is"),
                verbatimTextOutput("payment")
                )
        )
)
```

```
## Error: could not find function "shinyUI"
```


---

## Shinny App
### Server Side


```r
payment <- function(value, rate, term) {
        i <- (rate / 100) / 12
        n <- term * 12
        value * (i * (1 + i)^n) / ((1 + i)^n - 1) 
}

shinyServer(
        function(input, output) {
                output$payment <- renderPrint({payment(input$Value, input$rate, input$Term)})
        }
)
```

---

## THANK YOU!!
