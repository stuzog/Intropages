# The Fundamentals of R

## Four Fundamentals

The essence of R:

```{r}
R <- c(1:4)
R
```

(See [Vectors](#vectors) later).

**[One]** important difference about R:

* **Vector-based**: R is not a procedural language

**[Two]** reasons to use R for Data Science:

* **Designed for data**: R can manipulate big data sets
* **Graphics Are Graspable**: people understand graphical data

**[Three]**  fundamental principles of R per [John Chambers](https://en.wikipedia.org/wiki/John_Chambers_(statistician)):

* **Objects**: Everything that exists in R is an object
* **Functions**: Everything that happens in R is a function call
* **Interfaces**: to other softwares are an integral part of R

**[Four]** ways of programming R:

* **Command line**: entering R commands in a terminal
* **Source file**: running a set of commands from a saved file
* **R GUI interface**: available for Mac, WIndows, and Linux 
* **Code chunks in RStudio**: allows debugging as you write

## Basic Maths

R has all the basic mathematical functions:

```{r}

1 + 1

```

```{r}

1 + 2 + 3

```

```{r}

3 * 7 * 2

```

```{r}

4 / 3

```

R obeys the standard order of mathematical operations (**PEMDAS**):

1. **P**arentheses ( )
2. **E**xponents ^
3. **M**ultiplication x
4. **D**ivision \
5. **A**ddition +
6. **S**ubtraction -

```{r}

(2 ^ 5) + (2 * 5)

```

The use of white space between operators is recommended.

## Variables

Unlike statically-typed languages such a C++, R does not require variable types to be declared. An R variable can represent any data type or R object, such as a function, result, or graphical plot. R variables can be redeclared.

* Variable names can **contain alphanumeric characters**
  + but not **periods `.` or underscores `_`**
* **They cannot _start_ with a number or underscore**
* Variable names are **case sensitive**

### Assigning variables

R variable assignment operators are `<-` (default) and `=` (acceptable).

```{r}
x <- 2
x
```

```{r}
y = 5
y
```

You can also assign left-to-right with `->`, but variables are not often assigned that way.

```{r}
7 -> z
z
```

Assignment operations can be used successively to assign a value to multiple variables

```{r}
a <- b <- 42
a
b
```

You can also use the built-in `assign` function:

```{r}
assign("q", 4)
q
```

### Removing variables

`rm(variablename)` removes a variable.

```{r}
rm(q)
```

## Data Types

R has four main data types:

* Numeric
* Character (a.k.a Nominal)
* Date
* Logical

You can check the type of variable with `class(variablename`)

```{r}
x <- "eh?"
x
class(x)
```

```{r}
y <- 99
y
class(y)
```

### `Numeric` data types

Numeric data includes both integers and decimals ---  positive, negative, and zero --- similar to `float` or `double` in other languages. A numeric value stored in a variable is automatically assumed to be numeric in R.

You can test whether data is numeric with `is.numeric()`:

```{r}
is.numeric(y)
```

And if it's an integer with ``is.integer()`:

```{r}
is.integer(y)
```

The response of `FALSE` is because to set an integer as a variable you must append the value with `L`:

```{r}
y <- 99L
is.integer(y)
```

R promotes `integers` to `numeric` when needed.

### `Character` data types

R handles Character data in two primary ways: as `character` and as `factor`. They are treated differently:

```{r}
x <- "data"
x
class(x)
```

and

```{r}
y <- factor("data")
y
```

The `levels` are attributes of that factor.

To find the length of a `character` (or `numeric`):

```{r}
nchar(x)
```

This does not work for `factor` data.

### `Date` data types

R has numerous types of dates. `Date` and `POSIXct` are the most useful.

```{r}
date1 <- as.Date("2018-03-28")
date1
class(date1)
as.numeric(date1)
```

and

```{r}
date2 <- as.POSIXct("2018-03-28 10:45")
date2
class(date2)
as.numeric(date2)
```

Using `as.numeric` also changes the underlying type:

```{r}
class(date1)
class(as.numeric(date1))
```

### `Logical` data types

`Logical`s can be either `TRUE` (`T` or `1`) or `FALSE` (`F`or 0). `T` and `F` are not recommended as they are simply shortcuts to `TRUE` and `FALSE` and can be overwritten, causing woe, anguish, mayhem, and rioting. (`TRUE` or `F`?)

Logical data types have a similar test function `is.logical()`:

```{r}
k <- TRUE
class(k)
is.logical(k)
```

## Data Structures

R data structures are containers for data elements:

* **Vectors** -- collections of only **_same-type elements_**
* **Matrices** -- rectangular containers of only **_same-type elements_**
* **Data Frames** -- contain **_many types of vectors_** , all of the same length
* **Arrays** -- Vectors with **_dimensions_** for each **_same-type element_**
* **Lists** -- containers for elements of **_multi-type data types_**

### Vectors

Vectors are the heart of R; it is a **vectorised language**. An R `Vector` is:

> **A collection of elements of the same type**.

**Operations are applied to each element of a vector without the need to loop through them**. This separates R from other programming languages and makes it most suited to manipulation and graphical presentation of data.

**Vectors do not have a dimension**: there is no `column` or `row` vector. Unlike `mathematical vectors` there is no difference between column or row orientation.

#### Creating a vector

Vectors are created with `c`, meaning "combine":

```{r}
x <- c(1, 2, 3, 4, 5, 6, 7, 8)
x
```

Operations are applied to all elements at once:

```{r}
x + 2
x -3
x * 2
x / 4
x^2
sqrt(x)
```

#### Vector creation shortcuts

```{r}
1:8
8:1
-3:4
4:-3
```

#### Accessing vector elements

Any element of a `Vector` can be directly access using [square brackets] to point to it:

```{r}
x
x[4]
x[8]
```

#### Counting within Vectors

You can check the length of a vector:

```{r}
x
length(x)
y
length(y)
length(x + y)
```

and count the number of charactors in a vector:

```{r}
q <- c("One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight")
q
nchar(q)
```

#### Combining Vectors

Two vectors of the same or different length can be combined:

##### Vectors of the same length

```{r}
x <- 1:8
x
y <- -3:4
y
x + y
x - y
x * y
x / y
x^y
```

##### Vectors of different lengths

**For two `vectors` of different lengths, the shorter vector is recycled**, and R may issue a warning:

```{r}
x + c(1, 2)
x + c(1, 2, 3)

```

#### Comparison of two Vectors

```{r}
x <- c(1:8)
x
x > 5
y <- c(3:10)
y
x > y
```

The `all()` function tests whether all elements are `TRUE`

```{r}
x <-  10:1
y <-  -4:5
x
y
all(x < y)
```
The `any()` function tests is any element is 'TRUE`:
 
```{r}
any(x < y)
```
 
including vectors, matrices, data frames (similar to datasets), and lists (collections of objects).

#### Factor Vectors

`Factors` are an important concept in R. **`Factors` contain `levels`**, which are the unique values of that `factor` variable.

```{r}
q
qFactor <- as.factor(q)
qFactor
```

Note that the order of `levels`does not matter unless the `ordered` argument is set `TRUE`:

```{r}
factor(x=c("High School", "Doctorate", "Masters", "College"),
         levels=c("High School", "College", "Masters", "Doctorate"),
         ordered=TRUE)
```

### Matrices

A familiar mathematical structure, `matrices` are essential to statistics.

> A `Matrix` is a rectangular structure of rows and columns in which every element is of the same type, often all [numerics](#numeric-data-types).

`Matrics` can be acted upon similarly to `Vectors`, with **PEDMAS**-style element-by-element addition, subtraction, division, and equality.

#### Creating a Matrix

```{r}
A <- matrix(1:12, nrow=3)
A
```

Any element of a `matrix`can be directly accessed using [square bracket] co-ordinates:

```{r}
A[2,3]
A[3,4]
```

#### Dimensions of a Matrix

```{r}
nrow(A)
ncol(A)
dim(A)
```

#### Adding Matrices

```{r}
A
```

```{r}
B <-  matrix(13:24, nrow=3)
B
```

```{r}
A + B
```

#### Multiplying Matrices

```{r}
A * B
```

#### Logical querying

```{r}
A == B
```

#### Naming rows and columns

```{r}
colnames(A) <- c("A1", "A2", "A3", "A4")
rownames(A) <- c("First", "Second", "Third")
A
A["First", "A2"]
A[1,2]
```

Two special `vectors` -- `letters` and `LETTERS` -- create lowercase and UPPERCASE letter named matrix columns or rows:

```{r}
C <- matrix(21:40, nrow=2)
colnames(C) <- LETTERS[1:10]
rownames(C) <- c(letters[1:2])
C
```

### Dataframes

The `data.frame` is perhaps the primary reason for R's growing popularity as a powerful, focussed, and flexible language for use in all aspects of Data Science.

> A `data.frame` is a rectangular collection of [vectors](#vectors), all of which are of the same length but [differing data types](#data-types).

A `Data Frame` looks like an **Excel spreadsheet** in that the data is organised into __columns__ and __rows__. In statistical terms, each column is a _variable_ while each row contains specific _observations_. Similar to a [Matrix](#matrices) only in that it is also rectangular, a `data.frame` is a much more flexible and comprehensive data structure.

#### Creating a Dataframe

Using the existing functions:

```{r}
(x <- 8:1)
(y <- -3:4)
(q <- c("One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight"))
```

The simplest way of creating a `Dataframe` is with the `data.frame()` function:

```{r}
theDF <- data.frame(x, y, q)
theDF
```

This creates an 8x3 `data.frame` consisting of three `vectors`. Notice that the [data types](#data-types) are included below the column headings.

To assign names to the `vectors`:

```{r}
theDF <- data.frame(First=x, Second=y, Third=q)
theDF
```

To assign names to the rows:

```{r}
rownames(theDF) <- c("One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight")
theDF
```

#### Examining a Dataframe

The `nrow()`, `ncol()`, `dim()`, `rownames()`, and `names()` functions are available to investigate its properties:

```{r}
(nrow(theDF))
(ncol(theDF))
(dim(theDF))
(rownames(theDF))
(names(theDF))
```

Elements of any `vector` of a `data.frame` can be directly accessed using the `$` or `[row, col]` operators:

```{r}
(theDF$Second)
(theDF[7, 3])
```

To specify an entire row, leave out the column specification, _vice versa_ for specifying an entire column:

```{r}
(theDF[2, ])
(theDF[, 2])
```

To specify more than one row or column, use a `vector` of indices:

```{r}
(theDF[3:5, 2:3])
```

To specify multiple columns by name, use a `character vector` of the column names:

```{r}
(theDF[, c("First", "Third")])
```

To find the `class` of the entire `data.frame`:

```{r}
(class(theDF))
```

or the `class` of any `vector`:

```{r}
(class(theDF$Third))
```

#### Displaying a Dataframe

`data.frames` can be small, large, big, huge, or ginormous, depending on their size. The `head()` and `tail()` functions functions print only the first or last few rows, or the number of rows you set:

```{r}
(head(theDF))
(head(theDF, n=5))
(tail(theDF, n=5))
```


### Arrays

> An `Array` is a multidimensional [Vector](#vectors) whose elements are all the same type, but which also have attributes having dimensions (`dim`) that can also be named (`dimnames`).

#### Creating `Arrays`

To create an `Array`, the first element is the row index, the second the column index, and the remaining elements are for the outer dimensions `row`, `column`, `number of arrays`:

```{r}
theArray <- array(1:12, dim = c(2, 3, 2))
theArray
```

#### Accessing Arrays

Individual elements of an `Array` are accesssed using square brackets similar to a `Vector` but in this case by `[row, column, array #]`.

```{r}
theArray[1, , ]
theArray[2, , ]
theArray[1, , 1]
theArray[1, , 2]
theArray[, , 1]
theArray[, , 2]
```

### Lists

> `Lists` are used to store any number of items of any type: all `numeric` or all `character` vectors, or a mix of them; complete `data.frames`; and even other `lists`.

#### Creating Lists

`Lists` are created with the `list()` function. Each argument to the function becomes an element of the list:

```{r}
list(1, 2, 3)
```

Single-element lists can contain multi-element vectors:

```{r}
list(c(1, 2, 3))
```

Here's a two-element list with the second element a five-element `vector`:

```{r}
list1 <- list(c(1, 2, 3), 3:7)
list1
```

A two-element `list` with the first element an `array`, the second element a ten-element `vector`:

```{r}
list2 <- list(theArray, 1:10)
list2
```

#### Creating Empty Lists

Empty `lists` of a determined length are created using a `vector`:

```{r}
(emptyList <- vector(mode = "list", length = 4))
```

**Note**: Enclosing an expression in round brackets displays the results immediately after execution.

#### Naming Lists

`Lists` can have names, and each element of a `list` can have a unique name

```{r}
names(list2)
```

```{r}
(names(list2) <- c("The Array", "The Vector"))
list2

```

#### Naming List Elements

Names can also be assigned to `list` elements during creation using name-value pairs. This can also include naming the `list` itself:

```{r}
(list3 <- list(theARR=theArray, theVECT=1:10, List3=list2))
```

#### Adding To A List

New elements can be added to a `list` by appending a `numeric` or `named` index that does not yet exist:

```{r}
length(list3)
```

Adding a `numeric` index:

```{r}
list3[[4]] <- 11
length(list3)
list3
```

Adding a `named` index:

```{r}
list3[["AddedElement"]] <- 12:16
length(list3)
list3
```

