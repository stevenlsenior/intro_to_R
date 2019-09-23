Introduction to R
========================================================
author: Steven Senior
date: October 2019
autosize: true
font-family: 'Helvetica'
width: 1800
height: 1350

What is R?
========================================================
R is...
- A programming language (sort of)
- A statistical computing environment
- A way of life (some would say a cult)
- A free replacement for SPSS / Stata / SAS

R was created with the idea that people can start by using the built in functions and gradually progress to writing their own functions and programming.

That said, the learning curve can still feel a bit steep.


Why bother learning R?
========================================================

Reasons to bother:
- It's free!
- Coded analyses are more transparent and reproducible.
- It's widely used in industry, academia, and increasingly in public health.
- Processing 100 observations is as easy as processing 100,000.
- There's a package for everything.
- You can make some [cool things](https://shiny.rstudio.com/gallery/).
- Learning R involves learning to code, which is a useful skill.
- You like doing things the hard way.

Reasons not to bother:
- The learning curve is a bit steep.
- You're not going to do lots of quantitative stuff.
- You like paying lots for things you could get for free (although there are people who will sell you R).

Lessons from personal experience
========================================================

- Have a project (preferably lots).
- Learn to read the documentation.
- Learn to find help: 
   - [Stack Overflow](https://stackoverflow.com/), [Stack Exchange](https://stats.stackexchange.com/) etc.
   - Google (Googling the error message is totally legit programming skills)
- There are loads of free online resources. I made a [list] (https://medium.com/@steven.senior/free-r-resources-500182a54e90).

Installing R & R Studio
========================================================
**R**
- R is the basic programming environment. You need to install this first.
- R can be downloaded [here](https://cran.r-project.org/mirrors.html). Find the nearest mirror to you (for the UK, use Bristol or Imperial).
- Download the file for your operating system.

**R Studio**
- R Studio is an interactive development environment (IDE). It basically makes writing R code a lot easier. 
- You need R installed already for R Studio to work.
- You can download it [here](https://www.rstudio.com/products/rstudio/download/).

**R Studio Cloud**
- [R Studio Cloud](https://rstudio.cloud/) is a cloud-based version of R Studio that runs in a web browser.
- You don't need to install anything to use it. Just sign up for an account.
- It saves worrying about installing things. It also has links to a load of helpful learning resources.

Guided Tour of R Studio
========================================================

I'll go through this in the session, but if you couldn't join us, here's a [link](https://www.r-bloggers.com/a-tour-of-rstudio/) to a tour of RStudio.

The Working Directory 
========================================================

R projects typically need a folder in which to store data, scripts, and other things like images that it produces. This is the **working directory**. 

You can find out what R thinks the current working directory is using the `getwd()` function. You can change the working directory using `setwd("new_file_path")`. You can find out what's in the working directory using the `dir()` function.


```r
# Find out what the working directory is
getwd()
```

```
[1] "/cloud/project"
```

```r
# Find out what things are in the working directory
dir()
```

```
[1] "asthma.csv"                "imd_la.xlsx"              
[3] "intro_to_R.Rmd-figure"     "intro_to_R.Rmd-rpubs.html"
[5] "intro_to_R.Rmd.Rpres"      "project.Rproj"            
[7] "rsconnect"                
```

There are functions for creating, deleting, moving , downloading and checking if specific files exist. One useful one is `file.exists()`, which tells you if a file exists or not:


```r
# check if the 'asthma.csv' file exists
file.exists("asthma.csv")
```

```
[1] TRUE
```

Scripts & Writing Code
========================================================
You can do a lot just in the terminal. It's a good place to do quick exploratory stuff.

But one of the advantages of using a programming language is that you have a record of everything you have done to the data. Other people can re-use and check this. 

A **script** is just a list of commands. They're usually written in a text file with the file extension '.R'.

You can run individual lines from a script, chunks of it, or the whole thing. Select the code you want to run and press Ctrl + Enter. Commands are executed sequentially from top to bottom. 

Everything on a line after a `#` symbol will be ignored. Use these for writing comments to explain what your code is doing. This is a very good thing to do: it helps you come back to your code, and it helps other people try to figure out what on earth you've done.

R ignores white space. You can use this to make your code readable. Use as much as you like. The aim should be to make something that is easy for someone else to read. Everyone has their own style but things I tend to try to do:

- Put arguments in a function call on different lines.
- Make sure things are indented well and consistently.
- Object names that make sense.
- Stick to lower case!
- Avoid spaces and special characters in object and variable names.

I will probably break all of these rules in this set of slides.

Types of things in R
========================================================
R recognises a limited number of basic types of values:

- Numbers
- Characters (or 'strings', which are enclosed with "" or '' marks)
- Logical (`TRUE` or `FALSE`)
- Factors
- NA (usually for missing data)
- NaN (not-a-number - usually where an error has happened, like when you've tried to calculate `0/0`)

Objects
========================================================
R stores everything (single values, data, regression models, graphs) in things called **objects**.

An object is just a name (or key) plus some value.

Objects are created using the **assignment operator**: either `<-` or `=` (or if you want to be extra funky `->`). The name goes on left, the value on the right, like this

- `object_name <- object_value`.

Most R style guides (yes, there are such things!) recommend using <- because = is easily confused with `==`, which is R for 'are these two things the same'. The keyboard shortcut is 'Alt -'.

Objects can be accessed by typing their name and pressing return in the console.

*Example*

```r
# Create an object called 'name' with value 'Brockman'
name <- "Brockman"

# Access the object
name
```

```
[1] "Brockman"
```

Functions
========================================================

Functions are a type of object that produce outputs and may need inputs (called 'arguments').

Functions are followed by a pair of brackets that enclose the arguments, which are separated by a comma. They look like this: `function_name(argument_1, argument_2, ...)`

You call a function by typing its name and giving it the required inputs between the brackets. You can name the arguments (which I prefer to do for clarity) or just enter them in the order that the function expects. You can create a function like this:


```r
# create a function that returns the cube of a number minus the number squared
my_function <- function(x){
  result <- x^3 - x^2
  return(result)
}

# Test the function out
my_function(x = 7)
```

```
[1] 294
```

Some functions don't need any arguments (e.g. if all arguments have default settings). You still need to type the brackets though.


```r
# Sys.Date() tells us what day R thinks it is. It doesn't need inputs
Sys.Date()
```

```
[1] "2019-09-23"
```

You can get help on a function by typing `?function_name` (note no brackets!). This will include a list of all the arguments (including any defaults), an explanation of what it produces, and (ideally) some examples of how to use it.

The Environment
========================================================

- R does most of its work in memory. This means all of the objects and functions that R knows about aren't automatically saved to the hard disk. Instead they're kept in an **environment**. 
- You can find out what's in the environment with the `ls()` function. You can remove objects from the environment using `rm(object_name)`.


```r
# Find out what's in the environment
ls()
```

```
[1] "my_function" "name"       
```

```r
# Let's remove the 'name' object that we just created
rm(name)

# Now let's look at the environment again
ls()
```

```
[1] "my_function"
```

To start with you'll be operating in the **global environment**. There are other environments that exist and can be created but don't worry about those now. But it's worth knowing that objects created within a function are defined in a different environment. So you can't access the `result` object that we created earlier from the global environment:

















































































```
Error in eval(expr, envir, enclos) : object 'result' not found
```
