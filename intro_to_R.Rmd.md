Introduction to R
========================================================
author: Steven Senior
date: October 2019
autosize: true

What is R?
========================================================

- A programming language (sort of)
- A statistical computing environment
- A way of life (some would say a cult)


Why bother learning R?
========================================================

Reasons to bother:
- It's free!
- Coded analyses are more transparent and reproducible
- It's widely used in industry, academia, and increasingly in public health
- You can do almost anything with it: there's a package for everything

Reasons not to bother:
- The learning curve is a bit steep
- If you're not going to do lots of quantitative stuff
- If you like paying lots (although there are people who will sell you R)

Lessons from personal experience
========================================================

- Have a project (preferably lots)
- Learn to read the documentation
- Learn to find help: 
   - Stack Overflow
   - Google

Installing R & R Studio
========================================================

Guided Tour of R Studio
========================================================

Types of things in R
========================================================
R recognises a limited number of basic types of values:

- Numbers
- Characters (or 'strings', which are enclosed with "" or '' marks)
- Logical (`TRUE` or `FALSE`)
- Factors
- NA (usually for missing data)
- NaN (not-a-number - usually where an error has happened)

Objects
========================================================
R stores everything (single values, data, regression models, graphs) in things called **objects**.

An object is just a name (or key) plus some value.

Objects are created using the **assignment operator**: either `<-` or `=`

Most R style guides (yes, there are such things!) recommend using <- because = is easily confused with `==`, which is R for 'are these two things the same'. The keyboard shortcut is 'Alt -'.

Objects can be accessed by typing their name and pressing return in the console.

*Example*

```r
# Create an object called 'name' with value 'Steve'
name <- "Senior"

# Access the object
name
```

```
[1] "Senior"
```

Functions
========================================================

Functions are a type of object that produce outputs and may need inputs.

Functions are followed by a pair of brackets that enclose the inputs.

They look like this: `function_name(argument_1, argument_2, ...)`

You call a function by typing its name and giving it the required inputs between the brackets.

You can create a function like this:


```r
# create a function that returns the cube of a number minus the number squared
my_function <- function(x){
  x^3 - x^2
}

# Test the function out
my_function(7)
```

```
[1] 294
```

Some functions don't take any arguments. You still need to type the brackets though.


```r
# Sys.Date() tells us what day R thinks it is. It doesn't need inputs()
Sys.Date()
```

```
[1] "2019-09-20"
```


Vectors
========================================================
R stores data in objects called **vectors**.

A vector is just a collection of data **of the same type**

A vector's length is the number of items in it. You can get a vector's length using the `length()` function

Single data items are stored as vectors too - they're vectors with a length of 1.

Vectors are created using the `c()` function, or with dedicated functions for the type of data:
- `character()`
- `numeric()`
- `logical()`
- `factor()`

You can find out the type of vector using the `class()` function


```r
# Create a numeric vector
ages <- c(38, 39, 5, 2)

# Get the vector's length
length(ages)
```

```
[1] 4
```

```r
# Get the vector's class
class(ages)
```

```
[1] "numeric"
```

Lists
========================================================

Where vectors always have to contain the same type of data, a **list** can combine just about any set of objects.

Lists are used a lot to store complicated objects, like output from a regression model.

You probably won't use them much to start with but they're worth knowing about.

You can create a list with the `list()` function.


```r
# Make a list
my_list <- list(name, ages)

# Access the list
my_list
```

```
[[1]]
[1] "Senior"

[[2]]
[1] 38 39  5  2
```

You can access specific bits of the list like this:


```r
# Or using square brackets
my_list[[2]]
```

```
[1] 38 39  5  2
```

Data Frames
========================================================

**Data frames** are the most common format for data in R. You can think of them a bit like a spreadsheet.

A data frame is essentially a special type of list of vectors that **all have the same length**, but can contain different types of data. You can think of the individual vectors forming the columns of the spreadsheet. For epidemiological studies, the rows might represent individuals, and the columns represent the different types of data.

You can combine vectors into a data frame using the `data.frame()` function on the vectors.


```r
# Make some data
name <- c("Steven", "Vicki", "Oscar", "Imogen")
age <- c(38, 39, 5, 2)
sex <- c("male", "female", "male", "female")
can_drive <- c(TRUE, TRUE, FALSE, FALSE)

# Make a data frame
family <- data.frame(name, age, sex, can_drive)

# View the data frame
family
```

```
    name age    sex can_drive
1 Steven  38   male      TRUE
2  Vicki  39 female      TRUE
3  Oscar   5   male     FALSE
4 Imogen   2 female     FALSE
```

Data Frames
========================================================

There are lots of ways to view your data frames.
 - You can just call up the whole thing like we just did.
 - You can view the top or bottom few lines with the `head()` and `tail()` functions:

```r
# View the top two lines
head(family, n = 2)
```

```
    name age    sex can_drive
1 Steven  38   male      TRUE
2  Vicki  39 female      TRUE
```

```r
# View the bottom line
tail(family, n = 1)
```

```
    name age    sex can_drive
4 Imogen   2 female     FALSE
```
 - In RStudio you can get a sort of spreadsheet like view using the `View()` function (note the capital 'V'!)
 - You can get a quick summary of your variables using the `str()` function:

```r
# Get a summary of the data frame
str(family)
```

```
'data.frame':	4 obs. of  4 variables:
 $ name     : Factor w/ 4 levels "Imogen","Oscar",..: 3 4 2 1
 $ age      : num  38 39 5 2
 $ sex      : Factor w/ 2 levels "female","male": 2 1 2 1
 $ can_drive: logi  TRUE TRUE FALSE FALSE
```

Data Frames
========================================================
There are lots of ways to access specific bits of your data frames.

- You can use the index notation: `data_frame_name[row_number,column_number]`:


```r
# Get the first row
family[1,]
```

```
    name age  sex can_drive
1 Steven  38 male      TRUE
```

```r
# Get the third column
family[,3]
```

```
[1] male   female male   female
Levels: female male
```

```r
# Get the second data item in the third row
family[3, 2]
```

```
[1] 5
```
- Or you can get individual variables using the `$` operator: `data_frame_neme$variable_name`:


```r
# Get the 'can_drive' variable
family$can_drive
```

```
[1]  TRUE  TRUE FALSE FALSE
```

Tidy Data - A Digression
========================================================

Lots of time and effort goes into getting data into a form that you can actually use. 
Errors in data handling can really cock up a data analysis.
But most stats education doesn't cover how to manage data.
As we put more emphasis on reproducible analyses, principles of data handling are getting more attention.
Tidy data is just a set of simple principles to help guide data handling. These are:

- Each variable forms a column.
- Each observation forms a row.
- Each type of observational unit forms a table.

Following these principles makes manipulating the data a lot easier. 

Real data is often not tidy. Common problems include:

- Column headers are values, not variable names.
- Multiple variables are stored in one column.
- Variables are stored in both rows and columns.
- Multiple types of observational units are stored in the same table.
- A single observational unit is stored in multiple tables.

A fuller (but readable) overview is [here](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html).

Basic operations
========================================================
R can manipulate all of this data.

- Maths: all the usual stuff
- Strings: changing case, replacing letters, searching for matching strings, combining strings etc.
- Logical: asking whether two things are the same or not the same.

*Examples*

```r
# Get the log of age
log(family$age)
```

```
[1] 3.6375862 3.6635616 1.6094379 0.6931472
```

```r
# Convert names to lower case
tolower(family$name)
```

```
[1] "steven" "vicki"  "oscar"  "imogen"
```

```r
# Combine names with a surname
paste(family$name, "Senior", sep = " ")
```

```
[1] "Steven Senior" "Vicki Senior"  "Oscar Senior"  "Imogen Senior"
```

```r
# Find if age is two
family$age == 2
```

```
[1] FALSE FALSE FALSE  TRUE
```

Scripts & Writing Code
========================================================
You can do a lot just in the terminal. It's a good place to do quick exploratory things.

But one of the advantages of using a programming language is that you have a record of everything you have done to the data. Other people can re-use and check this. 

A **script** is just a list of commands. They're usually written in a text file with the file extension '.R`.

You can run individual lines from a script, chunks of it, or the whole thing. Commands in a script are executed sequentially from top to bottom.

Lines that start with a `#` symbol will be ignored. Use these for writing comments to explain what your code is doing. This is a very good thing to do: it helps you come back to your code, and it helps other people try to figure out what on earth you've done.

R ignores white space. You can use this to make your code readable. Use as much as you like. The aim should be to make something that is easy for someone else to read. Everyone has their own style but things I tend to try to do:

- Put arguments in a function call on different lines
- Make sure things are indented well and consistently
- object names that make sense
- Stick to lower case!
- Avoid spaces and special characters in object and variable names

```r
# Combine names with a surname
paste(family$name, 
      "Senior", 
      sep = " ")
```

```
[1] "Steven Senior" "Vicki Senior"  "Oscar Senior"  "Imogen Senior"
```

Loading Data
========================================================

Viewing Data
========================================================
- `head()`
- `summary()`
- `str()`
- `View()`

Saving Data
========================================================

Manipulating Data: Base R
========================================================

Manipulating Data: Tidyverse
========================================================

Basic Stats
========================================================
- Means, Medians, Modes, SD, Range, IQR etc.
- Summary()

Basic Plotting: Base R
========================================================

Basic Plotting: ggplot2
========================================================

More Stats: Common Tests
========================================================
- t-test & Wilcoxon
- Chi-squared
- Correlation

More Stats: Regression Models
========================================================
- `lm()`
- `glm()`
- `lmer()` and `glmer()`
