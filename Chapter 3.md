---
output:
  github_document: default
  html_document: default
---


```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```


```{r}
library(shiny)
```




```{r}
#Free text
ui <- fluidPage(
  textInput("name", "What's your name?"),
  passwordInput("password", "What's your password?"),
  textAreaInput("story", "Tell me about yourself", rows = 3)
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
#Numeric Input
ui <- fluidPage(
  numericInput("num", "Number one", value = 0, min = 0, max = 100),
  sliderInput("num2", "Number two", value = 50, min = 0, max = 100),
  sliderInput("rng", "Range", value = c(10, 20), min = 0, max = 100)
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
#Date
ui <- fluidPage(
  dateInput("dob", "When were you born?"),
  dateRangeInput("holiday", "When do you want to go on vacation next?")
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
#Limited choices
animals <- c("dog", "cat", "mouse", "bird", "other", "I hate animals")

ui <- fluidPage(
  selectInput("state", "What's your favourite state?", state.name),
  radioButtons("animal", "What's your favourite animal?", animals)
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
#Radio Button
ui <- fluidPage(
  radioButtons("rb", "Choose one:",
    choiceNames = list(
      icon("angry"),
      icon("smile"),
      icon("sad-tear")
    ),
    choiceValues = list("angry", "happy", "sad")
  )
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
ui <- fluidPage(
  selectInput(
    "state", "What's your favourite state?", state.name,
    multiple = TRUE
  )
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
ui <- fluidPage(
  checkboxGroupInput("animal", "What animals do you like?", animals)
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
ui <- fluidPage(
  checkboxInput("cleanup", "Clean up?", value = TRUE),
  checkboxInput("shutdown", "Shutdown?")
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
ui <- fluidPage(
  fileInput("upload", NULL)
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
ui <- fluidPage(
  actionButton("click", "Click me!"),
  actionButton("drink", "Drink me!", icon = icon("cocktail"))
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
#1 When space is at a premium, it’s useful to label text boxes using a placeholder that appears inside the text entry area. How do you call textInput() to generate the UI below?

ui <- fluidPage(
  titlePanel("Exercise 1"),
  textInput("name", "What's your name?", placeholder = "Your name"),
 
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)

```




```{r}

ui <- fluidPage(
titlePanel("Exercise 2"),
 sliderInput("dates", "Date Range:", 
              min = lubridate::as_date("2020-01-01"),
              max = lubridate::as_date("2020-12-31"),
              value = lubridate::today())

)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
ui <- fluidPage(
  titlePanel("Exercise 3"),
  selectInput("state", "Sub-headings:",
                list('List A' = animals,
                     'List B' = list(1,2,3,4,5)))
)


server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```





```{r}
ui <- fluidPage(
  titlePanel("Exercise 4"),
  sliderInput("rng", "Range", step = 5 , min = 0, max = 100, value = 0, animate = TRUE)
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)
```




```{r}
#Numeric Input
ui <- fluidPage(
  titlePanel("Exercise 4"),
  numericInput("number", "Select a value", value = 150, min = 0, max = 1000, step = 5)
 
)

server <- function(input, output, session) 
{
}
shinyApp(ui, server)

```



```{r}
ui <- fluidPage(
  textOutput("text"),
  verbatimTextOutput("code")
)
server <- function(input, output, session) {
  output$text <- renderText({ 
    "Hello friend!" 
  })
  output$code <- renderPrint({ 
    summary(1:10) 
  })
}

shinyApp(ui, server)

```


```{r}
ui <- fluidPage(
  textOutput("text"),
  verbatimTextOutput("code")
)
server <- function(input, output, session) {
  output$text <- renderText("Hello friend!")
  output$code <- renderPrint(summary(1:10))
}

shinyApp(ui, server)
```



```{r}
ui <- fluidPage(
  tableOutput("static"),
  dataTableOutput("dynamic")
)
server <- function(input, output, session) {
  output$static <- renderTable(head(mtcars))
  output$dynamic <- renderDataTable(mtcars, options = list(pageLength = 5))
}
shinyApp(ui, server)

```



```{r}
ui <- fluidPage(
  plotOutput("plot", width = "400px")
)
server <- function(input, output, session) {
  output$plot <- renderPlot(plot(1:5), res = 96)
}
shinyApp(ui, server)

```



```{r}
#1
ui <- fluidPage(
  titlePanel("Exercise 3.3.5.1"),
  plotOutput("plot", width = "700px", height = "400px")
)
server <- function(input, output, session) {
  output$plot <- renderPlot(plot(1:5), res = 96)
}
shinyApp(ui, server)
```


```{r}
ui <- fluidPage(
  titlePanel("Exercise 3.3.5.2"),
  fluidRow(
    column(6, plotOutput("plot1")),
    column(6, plotOutput("plot2"))
  )
)
server <- function(input, output, session) {
  output$plot1 <- renderPlot(plot(1:5))
  output$plot2 <- renderPlot(plot(1:5))
}

shinyApp(ui, server)
```



```{r}
ui <- fluidPage(
  dataTableOutput("table")
)
server <- function(input, output, session) {
  output$table <- renderDataTable(mtcars, options = list(pageLength = 5, ordering = FALSE, searching = FALSE))
}
shinyApp(ui, server)
```


```{r}
fluidPage(
  titlePanel("Hello Shiny!"),
  sidebarLayout(
    sidebarPanel(
      sliderInput("obs", "Observations:", min = 0, max = 1000, value = 500)
    ),
    mainPanel(
      plotOutput("distPlot")
    )
  )
)

server <- function(input, output, session) {
  
}
shinyApp(ui, server)


```



```{r}
library(shinythemes)

ui <- fluidPage(
  theme = shinythemes::shinytheme("cerulean"),
  titlePanel("Exercise 3.4.6.1"),
  headerPanel("Central limit theorem"),
  sidebarLayout(
    mainPanel(plotOutput("hist")),
    sidebarPanel(numericInput("m", "Number of samples:", 2, min = 1, max = 100))
  )
)

server <- function(input, output, session) {
  output$hist <- renderPlot({
    means <- replicate(1e4, mean(runif(input$m)))
    hist(means, breaks = 20)
  }, res = 96)
}

shinyApp(ui, server)
```



