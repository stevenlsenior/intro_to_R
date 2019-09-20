Introduction to R
========================================================
author: Steven Senior
date: October 2019
autosize: true
font-family: 'Helvetica'
width: 2400
height: 1350

What is R?
========================================================

- A programming language (sort of)
- A statistical computing environment
- A way of life (some would say a cult)


Why bother learning R?
========================================================

Reasons to bother:
- It's free!
- Coded analyses are more transparent and reproducible.
- It's widely used in industry, academia, and increasingly in public health.
- There's a package for everything.
- You can make some [cool things](https://shiny.rstudio.com/gallery/).
- You like doing things the hard way.

Reasons not to bother:
- The learning curve is a bit steep.
- You're not going to do lots of quantitative stuff.
- You like paying lots for things you could get for free (although there are people who will sell you R).

Lessons from personal experience
========================================================

- Have a project (preferably lots)
- Learn to read the documentation
- Learn to find help: 
   - Stack Overflow
   - Google
- There are loads of free online resources. I made a [list] (https://medium.com/@steven.senior/free-r-resources-500182a54e90).

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

Functions are a type of object that produce outputs and may need inputs (called 'arguments').

Functions are followed by a pair of brackets that enclose the arguments, which are separated by a comma.

They look like this: `function_name(argument_1, argument_2, ...)`

You call a function by typing its name and giving it the required inputs between the brackets. You can name the arguments (which I prefer to do for clarity) or just enter them in the order that the function expects

You can create a function like this:


```r
# create a function that returns the cube of a number minus the number squared
my_function <- function(x){
  x^3 - x^2
}

# Test the function out
my_function(x = 7)
```

```
[1] 294
```

Some functions don't need any arguments (e.g. if all arguments have default settings). You still need to type the brackets though.


```r
# Sys.Date() tells us what day R thinks it is. It doesn't need inputs()
Sys.Date()
```

```
[1] "2019-09-20"
```

You can get help on a function by typing `?function_name` (note no brackets!). This will include a list of all the arguments (including any defaults), an explanation of what it produces, and (ideally) some examples of how to use it.

Packages
========================================================

R has loads of built in functions. But part of the joy of R is that there is a wonderful community that have written code that you can re-use. These are bundled together in things called **packages**. 

A package is just a collection of functions and data, plus the documentation that goes with them.

You need to install the package the first time you use it. You do this with `install.packages()`.

You need to load the package into each new R session. You do this with `library()` or `require()` functions.


```r
# Install the readxl package - you only need to do this once!
install.packages("readxl")

# Load the readxl package - you need to do this each R session!
library(readxl)
```

Vectors
========================================================
R stores data in objects called **vectors**. A vector is just a collection of data **of the same type**.

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
fav_drink <- c("beer", "g&t", "juice", "milk")

# Make a data frame
family <- data.frame(name, age, sex, can_drive, fav_drink)

# View the data frame
family
```

```
    name age    sex can_drive fav_drink
1 Steven  38   male      TRUE      beer
2  Vicki  39 female      TRUE       g&t
3  Oscar   5   male     FALSE     juice
4 Imogen   2 female     FALSE      milk
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
    name age    sex can_drive fav_drink
1 Steven  38   male      TRUE      beer
2  Vicki  39 female      TRUE       g&t
```

```r
# View the bottom line
tail(family, n = 1)
```

```
    name age    sex can_drive fav_drink
4 Imogen   2 female     FALSE      milk
```
 - In RStudio you can get a sort of spreadsheet like view using the `View()` function (note the capital 'V'!)
 
Summary Functions
========================================================
The `summary()` function is very, very useful. It produces different outputs depending on the type of variable:

```r
# Summaries of numeric variables
summary(family$age)
```

```
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   2.00    4.25   21.50   21.00   38.25   39.00 
```

```r
# Summaries of character variables
summary(family$name)
```

```
Imogen  Oscar Steven  Vicki 
     1      1      1      1 
```

```r
# Summaries of factor variables
summary(as.factor(family$sex))
```

```
female   male 
     2      2 
```

```r
# Summaries of logical variables
summary(family$can_drive)
```

```
   Mode   FALSE    TRUE 
logical       2       2 
```

Summary Functions
========================================================
You can call `summary()` directly on the data frame.

```r
# Summarise all the things!
summary(family)
```

```
     name        age            sex    can_drive       fav_drink
 Imogen:1   Min.   : 2.00   female:2   Mode :logical   beer :1  
 Oscar :1   1st Qu.: 4.25   male  :2   FALSE:2         g&t  :1  
 Steven:1   Median :21.50              TRUE :2         juice:1  
 Vicki :1   Mean   :21.00                              milk :1  
            3rd Qu.:38.25                                       
            Max.   :39.00                                       
```

The `str()` function is also a useful way to preview the data:

```r
# Get a summary of the data frame
str(family)
```

```
'data.frame':	4 obs. of  5 variables:
 $ name     : Factor w/ 4 levels "Imogen","Oscar",..: 3 4 2 1
 $ age      : num  38 39 5 2
 $ sex      : Factor w/ 2 levels "female","male": 2 1 2 1
 $ can_drive: logi  TRUE TRUE FALSE FALSE
 $ fav_drink: Factor w/ 4 levels "beer","g&t","juice",..: 1 2 3 4
```

Data Frames
========================================================
There are lots of ways to access specific bits of your data frames.

- You can use the index notation: `data_frame_name[row_number , column_number]`:


```r
# Get the first row
family[1,]
```

```
    name age  sex can_drive fav_drink
1 Steven  38 male      TRUE      beer
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

Data Frames
========================================================
You can find out the names of the variables (i.e. columns) using the `names()` function:


```r
# Get the variable names
names(family)
```

```
[1] "name"      "age"       "sex"       "can_drive" "fav_drink"
```

You can find out the numbers of rows and columns using `nrow()` and `ncol()`:


```r
# Get the number of rows
nrow(family)
```

```
[1] 4
```

```r
# Get the number of columns
ncol(family)
```

```
[1] 5
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

Basic Operations
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

- Put arguments in a function call on different lines.
- Make sure things are indented well and consistently.
- Object names that make sense.
- Stick to lower case!
- Avoid spaces and special characters in object and variable names.

```r
# Combine names with a surname - contrast with earlier code
paste(family$name, 
      "Senior", 
      sep = " ")
```

```
[1] "Steven Senior" "Vicki Senior"  "Oscar Senior"  "Imogen Senior"
```

Loading Data - CSV Files
========================================================
Data comes in lots of weird and wonderful formats. There's usually a way to get them into R.

The easiest are comma-separated variable (.csv) files. You can read these in with `read.csv()`.

`read.csv` has a couple of annoying features: 
- Chief among them is its desire to convert every character variable to a factor. Thwart it by setting `stringsAsFactors = FALSE`. 
- You also want to tell it that the first row will be the variable names using `header = TRUE`.


```r
# Read the asthma csv file and store it as an object called 'asthma'
asthma <- read.csv(file = "asthma.csv",
                   stringsAsFactors = FALSE,
                   header = TRUE)

# View the top five rows
head(asthma,
     n = 5)
```

```
  X ID Age Sex Height Weight     Dadm    Ddisc
1 1  1   7   1    109   13.1 09/12/95 15/12/95
2 2  2   8   2    124   14.1 04/11/96 15/11/96
3 3  3   8   2    125   16.2 11/11/95 20/11/95
4 4  4   9   1    130   17.5 17/07/96 18/07/96
5 5  5  11   2    139   30.7 21/03/96 30/03/96
```

The `asthma.csv` file has a column (`X`) which are the row numbers. We don't need this, but we can get rid of it (more on this later...)

There are other basic formats (like tab-delimited data). These can be read in using `read.table()` (of which `read.csv()` is just a special case). You can specify what R looks for to separate the variables using the `sep` argument.

Loading Data - Excel Files
========================================================

Excel files are common, but can be a total pain in the arse (especially when people insist on using blank rows and putting random comments all over the place). 

R doesn't have a built in function for reading excel, but there are several packages that do. We already installed and loaded one (`readxl`). 

- Unless your data is on the first sheet, you need to tell it which sheet to open.
- You can skip the top n rows using the `skip` argument.


```r
# Read in the 'imd_la.xlsx' fileand store as an object called 'imd'
imd <- read_excel(path = "imd_la.xlsx",
                  sheet = 2,
                  skip = 0)

# View the top 4 rows
head(imd,
     n = 4)
```

```
# A tibble: 4 x 12
  `Upper Tier Loc… `Upper Tier Loc… `IMD - Average … `IMD - Rank of …
  <chr>            <chr>                       <dbl>            <dbl>
1 E06000001        Hartlepool                 21887.               28
2 E06000002        Middlesbrough              23563.               16
3 E06000003        Redcar and Clev…           19716.               55
4 E06000004        Stockton-on-Tees           17047.               84
# … with 8 more variables: `IMD - Average score` <dbl>, `IMD - Rank of
#   average score` <dbl>, `IMD - Proportion of LSOAs in most deprived 10%
#   nationally` <dbl>, `IMD - Rank of proportion of LSOAs in most deprived
#   10% nationally` <dbl>, `IMD - Extent` <dbl>, `IMD - Rank of
#   extent` <dbl>, `IMD - Local concentration` <dbl>, `IMD - Rank of local
#   concentration` <dbl>
```

Other Formats
========================================================

People still insist on using other stats packages. They will learn. But in the meantime, we're going to have to be able to read in other data formats. 

There are packages for this. A good one is the `foreign` package. This contains functions for reading a range of files including SPSS files. If you need to read Stata .dat files, the imaginatively titled `read.stata` and `read.stata13` packages are the ones you need.

As ever, Google is your friend.

Saving Data
========================================================

You may want to save your data (for example if you've spent ages pulling different variables together and manipulating them, and your code takes ages to run). You can save in most formats, but I recommend using csv for simplicity. You can save data using the `write.csv()` function.


```r
# Save the asthma object to a new csv file called 'asthma_new.csv`
write.csv(x = asthma,                # the object you want to save
          file = "asthma_new")       # the file name you want to five it
```

Manipulating Data: Base R
========================================================

You will probably want to select, delete, and transform data. There are lots of ways to do this. 

- You can rename your variables simply by assigning a new value to the names attribute of the data frame using `names()`:

```r
# Rename a variable
names(family)[4] <- "driver"
```
- You can add a new variable by assigning the vector directly to a new variable using the `$` operator

```r
# Add a new variable
family$middle_name <- c("Lee", "Louise", "Brian", "Emmeline")
```
- You can drop columns or rows using the square brackets operator with a `-` sign:

```r
# Drop the 'fav_drink' variable
family <- family[,-5]

# See what we've created
family
```

```
    name age    sex driver middle_name
1 Steven  38   male   TRUE         Lee
2  Vicki  39 female   TRUE      Louise
3  Oscar   5   male  FALSE       Brian
4 Imogen   2 female  FALSE    Emmeline
```

Manipulating Data: Tidyverse
========================================================
Base R is fine, particularly for quick manipulations. But it can quickly get dense and confusing when you need to do repeated manipations on the same data frame.

The `tidyverse` is an enormous package of packages that contains functions built around the principles of tidy data.

The functions in `tidyverse` are named and designed to make code easier to read.
One package within `tidyverse` is called `dplyr`. This package makes manipulating and summarising data in R *much* easier.

In particular, it introduces the `%>%` (pipe operator). This lets you pass the outputs from one function straight to another. This means you can omit the first argument (which is normally the data frame that you want to operate on).


```r
# load the tidyverse
library(tidyverse)

# manipulate the asthma data and store over the old object
asthma <- asthma %>%
          select(-X) %>%                                         # Drop that pesky extra variable
          mutate(Dadm = as.Date(Dadm, format = "%d/%m/%y"),      # Convert variables to date variables
                 Ddisc = as.Date(Ddisc, format = "%d/%m/%y"),
                 los = Ddisc - Dadm)                             # Calculate a length of stay variable

# Summarise by sex
asthma %>% 
  group_by(Sex) %>%                                
  summarise(mean_height = mean(Height),            
            mean_weight = mean(Weight),
            mean_age = mean(Age),
            mean_los = mean(los))
```

```
# A tibble: 2 x 5
    Sex mean_height mean_weight mean_age mean_los     
  <int>       <dbl>       <dbl>    <dbl> <drtn>       
1     1        140.        25.1     11.2 4.750000 days
2     2        144.        31.3     11.8 7.166667 days
```

Basic Stats
========================================================
R is a stats language. So you'd expect that it has plenty of built-in functions for calculating routine stats: These include `mean()`, `sd()`, `median()`, `range()`, `IQR()`, `mode()`. We've used a couple of these already.

Helpfully, the `summary()` function produces lots of these in one go:


```r
# Summarise the ages in the 'Age' variable
summary(asthma$Age)
```

```
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   7.00    8.25   11.50   11.60   14.50   17.00 
```

Similarly there are built in functions for common statistical tests. These include `t.test()`, `wilcox.test()`,  `chisq.test()`, and `cor.test()`.

```r
# Compare length of stay by sex
t.test(formula = los ~ Sex,
       data = asthma)
```

```

	Welch Two Sample t-test

data:  los by Sex
t = -0.97132 days, df = 5.6929, p-value = 0.3708 days
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -8.585158 days  3.751824 days
sample estimates:
Time differences in days
mean in group 1 mean in group 2 
       4.750000        7.166667 
```

Basic Stats - More Examples
========================================================
There are two functions for correlation - `cor()` just gives you the coefficent. `cor.test()` gives you the full hypothesis test.

```r
# Get the correlation coefficient
cor(x = asthma$Height, y = asthma$Weight)
```

```
[1] 0.9070978
```

```r
# Correlate height and weight
cor.test(x = asthma$Height, y = asthma$Weight)
```

```

	Pearson's product-moment correlation

data:  asthma$Height and asthma$Weight
t = 6.0954, df = 8, p-value = 0.000291
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 0.6469869 0.9780995
sample estimates:
      cor 
0.9070978 
```

More Stats: Regression Models
========================================================
- `lm()`
- `glm()`
- `lmer()` and `glmer()`

Basic Plotting: Base R
========================================================

One of the reasons that people like R is that it can produce high quality graphics. It's used by a lot of data visualisatoin people and data journalists for this reason.

R has built in plotting functions. These are fine for quick exploratory plots. They often require fewer lines of code, and can be built up interactively.

The basic functions are `plot()` and `hist()` and `boxplot()`.


```r
# Get a histogram of lengths of stay
hist(as.numeric(asthma$los))
```

<img src="intro_to_R.Rmd-figure/unnamed-chunk-29-1.png" title="plot of chunk unnamed-chunk-29" alt="plot of chunk unnamed-chunk-29"  />

Basic Plotting: Base R
========================================================


```r
# Box plot of weight by Sex
boxplot(Weight ~ Sex,
        data = asthma)
```

<img src="intro_to_R.Rmd-figure/unnamed-chunk-30-1.png" title="plot of chunk unnamed-chunk-30" alt="plot of chunk unnamed-chunk-30"  />

Basic Plotting: Base R
========================================================


```r
# Get plot height against weight
plot(formula = Height ~ Weight,
     data = asthma)

# Fit a regression model
m1 <- lm(formula = Height ~ Weight,
         data = asthma)

# Add a regression line
abline(m1, col = "red")
```

<img src="intro_to_R.Rmd-figure/unnamed-chunk-31-1.png" title="plot of chunk unnamed-chunk-31" alt="plot of chunk unnamed-chunk-31"  />

Plotting: ggplot2
========================================================

The `ggplot2` package is part of the `tidyverse`. It  produces better looking graphs than base R, but these graphs often need more lines of code to build up, and the language takes a little getting used to. The book on ggplot is available free [here](https://ggplot2-book.org/).

The `ggplot()` function requires a set of aesthetic mappings from data to attributes of the plot (position, colour, size)


```r
# Scatter plot using ggplot
g1 <- ggplot(aes(x = Height,
                 y = Weight,
                 colour = Sex,
                 size = as.numeric(los)),
             data = asthma) +
      geom_point() +
      scale_fill_viridis_d() +
      theme_bw() +
      theme(plot.title = element_text(face = "bold")) +
      labs(title = "Scatterplot of asthma data",
           subtitle = "Plot subtitle",
           caption = "Plot caption",
           x = "Height (cm)",
           y = "Weight (kg)")

g1
```

![plot of chunk unnamed-chunk-32](intro_to_R.Rmd-figure/unnamed-chunk-32-1.png)

