PS1 - Solution
================
Solution

### Problem 1: Markdown output

Complete MDSR (your book) Appendix D exercises D.1-D.4 (3-6 in the
second edition) without actually running the R chunk code given. Briefly
explain why the code gives the output that you claim it will give.

#### D.1 \[second edition problem 3\]

What is output?

*answer:* In the Markdown doc, all 3 chunks of code will appear and the
output of 2, 3, 4, 5, 6 will be displayed.

#### D.2 \[second edition problem 5\]

What is output?

*answer:* In the Markdown doc, none of the chunks of code will appear
but we will see the output of 2, 3, 4, 5, 6 from the third chunk.

#### D.3 \[second edition problem 6\]

What is output?

*answer:* In the Markdown doc, only code from chunk 3 will appear and
the output of 1, 2, 3, 4, 5 will be displayed.

#### D.4 \[second edition problem 4\]

What is output?

*answer:* In the Markdown doc, no output will appear.

### Problem 2: Inline R code

Consider the following R chunk and sentence with inline R code (which
you can see in the .Rmd file):

``` r
> first <- "Foo"
> last <- "Fu"
```

**Sentence:** The bunny is named Foo.

Consider the following four commands:

1.  `c(first,last)`
2.  `first last`
3.  `paste(first,last)`
4.  `paste0(first,last)`

For (1)-(4), replace the object `first` in the sentence above with the
given command. Explain the following:

- Which command (1)-(4) gives you an error? Why? (you’ll need to omit
  this inline R code to knit your document!)
- Explain the differences in output produced by the other three
  commands.

*answer:*

- Command 2 gives an error:

1.  The bunny is named Foo, Fu.
2.  error
3.  The bunny is named Foo Fu.
4.  The bunny is named FooFu.

- This will produce the error because simply entering two vectors
  constitutes two commands that produce two outputed objects not one.
  All other commands produce one object.

Note: In one line of code, two separate commands would need to be
separated by `;`. In Markdown inline code is looking for one command. If
you try entering `first; last` the output shown will be the last command
entered: Fu The vector entry gives the vector entries separated by
commas. Both paste commands both paste together the character strings,
but `paste` defaults to include a space in between the entries you are
pasting while `paste0` defaults to include no space.

### Problem 3: Logical vectors

Suppose we have a list of food (carrot, orange, m&m, apple, candy corn)
that we characterize by color (orange or not) and candy (candy or not).
Here are the data vectors describing each food:

``` r
> orange <- c(TRUE, TRUE, FALSE, FALSE, TRUE)
> candy <- c(FALSE, FALSE, TRUE, FALSE, TRUE)
> table(orange, candy)
       candy
orange  FALSE TRUE
  FALSE     1    1
  TRUE      2    1
```

**1.** What type of food does the product of these vectors represent?
(e.g. what does `x` of 0 mean? what does 1 mean?)

``` r
> x<- orange*candy
> x
[1] 0 0 0 0 1
```

*answer:* This produces a vector that indicates an food that is “orange
and candy” (intersection) with a 1 and all other types with a 0.

**2.** What type of food does the sum of these vectors represent?
(e.g. what does `x` of 0 mean? what does 1 mean? a 2?)

``` r
> y <- orange + candy
> y
[1] 1 1 1 0 2
```

*answer:* This produces a vector that identifies an food that is “orange
and candy” (intersection) with a 2, neither orange nor candy with a 0,
and all other types (orange, not candy or candy, not orange) with a 1.

**3.** What type of food does expression below represent? (e.g. what
does 0 mean? 1? -1? -2?)

``` r
> y*(-1)^orange
[1] -1 -1  1  0 -2
```

*answer:* This produces a vector that identifies all four combos of
orange and candy: food that is “orange and candy” (intersection) is a
-2, neither is a 0, orange/not candy is a -1 and candy/not orange is a
1.

### Problem 4: Object classes and errors

Complete Appendix exercises B.1 and B.9 (3 and 10 in the second
edition). For exercise B.1, both describe what is returned and explain
why that command produces the object. Try to answer these questions
without using R, but you can use R to help or verify your answer.
(e.g. This would be practice for an exam where you can’t use R!)

#### B.1

What objects are returned?

*answer:*

- `obj1*10` will multiple each entry in the `obj1` vector by the scalar
  (length 1 vector) 10. Output will look like `20,30,...,100`
- `obj1[2:4]` will return the 2nd, 3rd and 4th entries in `obj1`. Output
  will look like `3,4,5`
- `obj1[-3]` will return everything except the 3rd entry in `obj`.
  output will look like `2,3,5,6,7,8,9,10`
- `obj1 + obj2` will start by adding the 1st and 2nd entries in each
  vector. But then we run out of entries in `obj2` so R will start
  recycling entries and add the 3rd and 4th entries in `obj1` to the 1st
  and 2nd entries in `obj2`. This repeats until all `obj` entries have
  been used. Output (with a warning) will look like
  `4, 8, 6, 10, 8, 12, 10, 14, 12`
- `obj1*obj3` same idea as the previous answer except with
  multiplication instead of addition. Output will look like
  `2, 0, 4, 0,...`
- `obj1 + obj4` will add the `obj4` value to each entry in `obj1` (much
  like the recycling done in the previous two answers, except this is
  “allowable”” arithmetic so there is no error message). Output looks
  like `44,45,46,...`
- `obj2 + obj3` artihmetic with a logic (T/F) vector assigns a 0 value
  to F and 1 to T. So the output returned will be `3,5`
- `sum(obj2)` This just sums the values of `obj2`. Output is `7`.
- `sum(obj3)` This just sums the values of `obj3`. Output is `1`.

Code to check work:

``` r
> obj1 <- 2:10
> obj2 <- c(2,5)
> obj3 <- c(TRUE,FALSE)
> obj4 <- 42
> obj1*10
[1]  20  30  40  50  60  70  80  90 100
> obj1[2:4]
[1] 3 4 5
> obj1[-3]
[1]  2  3  5  6  7  8  9 10
> obj1 + obj2
Warning in obj1 + obj2: longer object length is not a multiple of shorter object
length
[1]  4  8  6 10  8 12 10 14 12
> obj1*obj3
Warning in obj1 * obj3: longer object length is not a multiple of shorter object
length
[1]  2  0  4  0  6  0  8  0 10
> obj1 + obj4
[1] 44 45 46 47 48 49 50 51 52
> obj2 + obj3
[1] 3 5
> sum(obj2)
[1] 7
> sum(obj3)
[1] 1
```

#### B.9

What objects are returned?

*answer:*

- `result1 <- sqrt 10` error: `sqrt` is a function that needs `()`
- `result2 <-- "Hello to you!"` error: extra `-` sign used for
  assignment operator. This would actually be fine if you were assigning
  a numeric/integer value as it would be treated as a negative sign.
- `3result <- "Hello to you"` error: you can’t start a variable name
  with a number
- `result4 <- "Hello to you` error: missing the end `"`
- `result5 <- date()` no error. `data()` is a function that doesn’t take
  in any values, it simply returns the current date.

### Problem 5: Object classes and data types

Complete Appendix exercise B.2 (9 in the second edition). In addition to
describing the *class* of object returned by each command, you should
explain the *data type(s)* in each object (e.g. are entries numeric?
character? etc). Try to answer these questions without using R, but you
can use R to help or verify your answer. (e.g. This would be practice
for an exam where you can’t use R!)

#### B.2

Describe the class of objects as well as its data type

*answer:*

- `data.frame(a,b,c)` returns a `data.frame` class object with variable
  values given by `a,b,c` (numeric, logical, factor).
- `cbind(a,b)` returns a `matrix` object with columns equal to `a` and
  `c(1,0)` because it will force the logical vector `b` into a numeric
  vector (all entries in a `matrix` must be the same type of values.)
- `rbind(a,b)` returns a `matrix` object with numeric rows equal to `a`
  and `c(1,0)`.
- `cbind(a,b,c)` returns a `matrix` object with columns equal to
  **character** expressions of `a`, `b`, and `c`. Again, a matrix needs
  to have entries that are the same type of values. Since you included
  the character vector `c` in the matrix it assumes that everything in
  it is a character (it can’t force a character vector to be represented
  by something numeric).
- `list(a,b,c)[[2]]` returns a `logical` object because the logical
  vector `b` is the 2nd element in the list.

Code to check work:

``` r
> a <- c(10,15)
> b <- c(TRUE, FALSE)
> c <- c("happy","sad")
> data.frame(a,b,c)
   a     b     c
1 10  TRUE happy
2 15 FALSE   sad
> cbind(a,b)
      a b
[1,] 10 1
[2,] 15 0
> rbind(a,b)
  [,1] [,2]
a   10   15
b    1    0
> cbind(a,b,c)
     a    b       c      
[1,] "10" "TRUE"  "happy"
[2,] "15" "FALSE" "sad"  
> list(a,b,c)[[2]]
[1]  TRUE FALSE
```

### Problem 6: Lists

Consider the list below.

``` r
> mylist <- list(x1="sally", x2=42, x3=FALSE, x4=1:5)
```

Show how to produce the following output in **one command**:

1.  `"sally"` (atomic character vector of length 1)
2.  `42` (atomic numeric vector of length 1)
3.  the 3rd and 4th entries in `x4` (atomic numeric vector of length 2)
4.  the length of `x4`

*answer:*

1.  The book uses `mylist[["x1"]]` to get `"sally"`. Possible other ways
    include `mylist$x1`, `mylist[[1]]` and `mylist[1][[1]]`. The last
    command (which I wouldn’t suggest using) returns a list with “x1” as
    its only entry, you then access the into in the first entry with
    `[[1]]`.
2.  The book uses `mylist$x2` to get 42. Other ways include
    `mylist[[2]]`, `mylist[["x2"]]` and `mylist[2][[1]]`
3.  Possible ways include `mylist$x4[3:4]`, `mylist[[4]][3:4]`,
    `mylist[["x4"]][3:4]`
4.  The book uses `length(mylist[["x4"]])`. Possible other ways include
    `length(mylist$x4)` and `length(mylist[[4]])`

Code to check work:

``` r
> # 1
> mylist$x1
[1] "sally"
> mylist[1][[1]]
[1] "sally"
> mylist[[1]]
[1] "sally"
> # 2
> mylist[[2]]
[1] 42
> mylist[["x2"]]
[1] 42
> mylist[2][[1]]
[1] 42
> # 3
> mylist$x4[3:4]
[1] 3 4
> mylist[[4]][3:4]
[1] 3 4
> mylist[["x4"]][3:4]
[1] 3 4
> # 4
> length(mylist$x4)
[1] 5
> length(mylist[[4]])
[1] 5
```

### Problem 7: More lists

Use the same list as problem 6. What type of objects are produced with
the following commands:

1.  `mylist[1]`
2.  `mylist[[1]]`
3.  `unlist(mylist)`

*answer:*

1.  `mylist[1]` returns the first entry (which is a character vector of
    length 1) in `mylist` in list form (it preserved the original class
    of `mylist`).
2.  `mylist[[1]]` returns an object that equals the first entry in
    `mylist`, so the type of object that it returns is a character
    vector of length 1.
3.  `unlist(mylist)` returns a vector of all values stored in `mylist`.
    Because there is one character entry, the type of vector will be
    character.

Code to check work:

``` r
> str(mylist[1])
List of 1
 $ x1: chr "sally"
> str(mylist[[1]])
 chr "sally"
> str(unlist(mylist))
 Named chr [1:8] "sally" "42" "FALSE" "1" "2" "3" "4" "5"
 - attr(*, "names")= chr [1:8] "x1" "x2" "x3" "x41" ...
```

### Problem 8: Yet more lists

Use the same list as problem 6. Suppose you want to add a vector `x5` to
`mylist` so `mylist` has length 5. You try two ways of doing this, shown
below. Carefully describe and show the object that is produced by each
of these commands and explain whether the command produces your desired
list.

1.  `mylist <- list(mylist, x5=c(1,-7,3))`
2.  `mylist$x5 <- c(1,-7,3)`

*answer:*

1.  This command will create a new list that is composed of two entries:
    the first entry `newlist[[1]]` is the previous list given by
    `mylist` and the second entry `newlist[[2]]` is the vector `x5` that
    we want to add. So this command creates a list of a list and vector.
2.  This command will add the vector `x5` as the 5th entry in the
    original list `mylist`. If you just want to add a new entry to a
    list, this would be the way to do it.

Note: this list behavior is a little different than other object types.
e.g. if you run a command like
`data.frame(old.dataframe, x5=new.variable)` you create a data frame
that is identical to `old.dataframe` but with a new column variable
`new.variable` added. An equivalent way of doing this is with
`old.dataframe$new.variable <- x5`. But when dealing with `lists` these
two types of commands produce different results.

Code to check work:

``` r
> newlist<- list(mylist, x5=c(1,-7,3))
> newlist
[[1]]
[[1]]$x1
[1] "sally"

[[1]]$x2
[1] 42

[[1]]$x3
[1] FALSE

[[1]]$x4
[1] 1 2 3 4 5


$x5
[1]  1 -7  3
> newlist[[1]]
$x1
[1] "sally"

$x2
[1] 42

$x3
[1] FALSE

$x4
[1] 1 2 3 4 5
> newlist[[2]]
[1]  1 -7  3
> mylist$x5 <- c(1,-7,3)
> mylist
$x1
[1] "sally"

$x2
[1] 42

$x3
[1] FALSE

$x4
[1] 1 2 3 4 5

$x5
[1]  1 -7  3
```
