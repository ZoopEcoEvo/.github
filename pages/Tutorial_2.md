Part 2 - More Data Manipulation
================
Matthew Sasaki

- <a href="#rbind-and-cbind" id="toc-rbind-and-cbind">rbind() and
  cbind()</a>
- <a href="#summarizing-data-frames-with-table"
  id="toc-summarizing-data-frames-with-table">Summarizing data frames with
  table()</a>
- <a href="#the-for-loop" id="toc-the-for-loop">The <em>for loop</em></a>
  - <a href="#modifying-the-for-statement"
    id="toc-modifying-the-for-statement">Modifying the for statement</a>
    - <a href="#the-counter" id="toc-the-counter">The counter</a>
- <a href="#if--else-statements" id="toc-if--else-statements">If / Else
  statements</a>
- <a href="#while-statements" id="toc-while-statements">While
  Statements</a>

Hopefully you’re now familiar with the basic syntax of R and the
structure of common data objects. As we saw in the first tutorial, both
are important when manipulating data in what might seem like simple ways
(e.g. - subsetting rows or columns in a dataframe). This section of the
tutorial will further develop your ability to manipulate and analyze
data using slightly more complicated code structures.

# rbind() and cbind()

Even when you’re importing data files from excel or .csv files, you may
need to combine data objects in R during an analysis. There are two
straightforward ways to do this using base R; rbind() and cbind(). These
stand for “Row Bind” and “Column Bind” respectively. They’re perhaps
best illustrated when trying to add a vector to an array or data frame.
In the example below, the function rbind() will bind the vector to the
data frame as a new row, while cbind() will bind the vector to the data
frame as a new column. Note that the new column takes on the variable
names as a column name.

``` r
#Note that our vector is length 7, and that the array is a 7 x 7 grid
vector = c(3,3,3,3,3,3,3)
df = data.frame(matrix(nrow = 7, ncol = 7)) 

#Attaching vector as new row
rbind(df, vector)
##   X1 X2 X3 X4 X5 X6 X7
## 1 NA NA NA NA NA NA NA
## 2 NA NA NA NA NA NA NA
## 3 NA NA NA NA NA NA NA
## 4 NA NA NA NA NA NA NA
## 5 NA NA NA NA NA NA NA
## 6 NA NA NA NA NA NA NA
## 7 NA NA NA NA NA NA NA
## 8  3  3  3  3  3  3  3

#Attaching vector as new column
cbind(df, vector)
##   X1 X2 X3 X4 X5 X6 X7 vector
## 1 NA NA NA NA NA NA NA      3
## 2 NA NA NA NA NA NA NA      3
## 3 NA NA NA NA NA NA NA      3
## 4 NA NA NA NA NA NA NA      3
## 5 NA NA NA NA NA NA NA      3
## 6 NA NA NA NA NA NA NA      3
## 7 NA NA NA NA NA NA NA      3
```

These commands work for binding arrays/dataframes to other
arrays/dataframes too.

``` r
df1 = data.frame(matrix(nrow = 2, ncol = 4, data = 1))
df2 = data.frame(matrix(nrow = 2, ncol = 4, data = 2))

rbind(df1, df2)
##   X1 X2 X3 X4
## 1  1  1  1  1
## 2  1  1  1  1
## 3  2  2  2  2
## 4  2  2  2  2

cbind(df1, df2)
##   X1 X2 X3 X4 X1 X2 X3 X4
## 1  1  1  1  1  2  2  2  2
## 2  1  1  1  1  2  2  2  2
```

You might notice that when cbinding these two data frames, the resulting
object has **duplicate** column names. This is absolutely an issue. When
rbinding data frames, they must have the same column names, in the same
order, otherwise R will not allow the objects to be joined (we will
cover more flexible strategies for binding rows in a later tutorial).
However, when cbinding data frames, it’s important to make sure that the
columns either have different names before binding, or are renamed after
binding, to prevent confusion or interference with later analyses.
Re-naming columns has a slightly different syntax from anything we’ve
done so far.

``` r
colnames(df1) = c("col1", "col2", "col3", "col4")

rbind(df1, df2)
## Error in match.names(clabs, names(xi)): names do not match previous names

cbind(df1, df2)
##   col1 col2 col3 col4 X1 X2 X3 X4
## 1    1    1    1    1  2  2  2  2
## 2    1    1    1    1  2  2  2  2
```

You can also use a vector to store and assign column names.

``` r
names_for_columns = c("A", "B", "C", "D")

colnames(df2) = names_for_columns

cbind(df1, df2)
##   col1 col2 col3 col4 A B C D
## 1    1    1    1    1 2 2 2 2
## 2    1    1    1    1 2 2 2 2
```

# Summarizing data frames with table()

When dealing with categorical or non-numeric data, it can sometimes be
useful to summarize the contents of a data object in table format. The
table() function provides counts for each of the different categories or
factors contained within a column.

``` r
#Manually creating a data frame that contains information for five cats
cat_data = data.frame(name = c("MrWhiskers", "CatStevens", "ChairmanMeow", 
                               "FuzzAldrin", "UmaPurrman"), 
                      colour = c("black", "orange", "tabby", "tabby", "black"))

#Summarize the contents of the table by colour
table(cat_data$colour)
## 
##  black orange  tabby 
##      2      1      2
```

You now know that there are two black cats, one orange cat, and two
tabbies in the data frame. Now let’s say you wanted to print the names
of the different cats in each colour category. For a small data frame
like this, it’s probably not necessary to manipulate anything and you
could just print the dataframe to get the information you need. But when
data frames contain hundreds or thousands of observations, it’s
impractical to try to get the information you need just by reading
through the unaltered object. We’ve covered how to use logical
statements to subset data frames already, and you could use this
approach to identify which cats have which coloration. Make sure you are
comfortable with the subsets performed below.

``` r
black_cats = cat_data[cat_data$colour == "black",]
black_cats$name
## [1] "MrWhiskers" "UmaPurrman"

orange_cats = cat_data[cat_data$colour == "orange",]
orange_cats$name
## [1] "CatStevens"

tabby_cats = cat_data[cat_data$colour == "tabby",]
tabby_cats$name
## [1] "ChairmanMeow" "FuzzAldrin"
```

This strategy basically copies, pastes, and slightly alters code for
each category. When dealing with small numbers of categories, this is
manageable (if a little inefficient), but what if you have twenty
categories? A hundred? It rapidly becomes infeasible to replicate code
for large numbers of categories. To solve this issue, we use a code
structure called a ““for loop”“.

# The *for loop*

A “for loop” is a simple way to run the same chunk of code many times on
different data, without having to copy, paste, and modify the code. As
such, the “for loop” is often essential for keeping code manageable. A
“for loop” has two components, the “for” statement, and the “code
chunk”. The code chunk is the code you want to run. While this is of
course an important component of the “for loop”, the for statement is
what’s really at the heart of this coding structure. The for statement
simply establishes a variable and controls its identity. In the example
below, the for statement is saying that there is some variable ‘i’,
which is going to cycle through values from 1 to 10. The code chunk will
then iterate, or repeat, with each of those different values assigned to
i. These two different components follow a set syntax of
for(statement){code_chunk}, but it’s common to see the code chunk split
across multiple lines, with the first curly bracket following the for
statement, and the code itself below that.

``` r
for(i in 1:10){
  print(i)
}
## [1] 1
## [1] 2
## [1] 3
## [1] 4
## [1] 5
## [1] 6
## [1] 7
## [1] 8
## [1] 9
## [1] 10
```

The trick with “for loops” is figuring out how to write the code chunk
to use the variable instead of fixed values to accomplish your goal.
It’s important to note that each iteration is independent; what happens
in one iteration doesn’t get carried forward to the next iterations
(automatically). Going back to our feline dilemma, we still want to know
the names of the different cats that have each type of coloration. A
common approach for using “for loops” to analyze data in this way is to
start off by identifying all of the unique groups, and then using a “for
loop” to cycle through each one to analyze the data. Look through the
example below. Try to figure out what each line of code is doing, and
how the “for loop” structure produces the printed results. A commented
version is included afterwards if you get stuck.

``` r
cat_colours = unique(cat_data$colour)

for(c in 1:length(cat_colours)){
  subset = cat_data[cat_data$colour == cat_colours[c],]
  print(c(cat_colours[c], subset$name))
}
## [1] "black"      "MrWhiskers" "UmaPurrman"
## [1] "orange"     "CatStevens"
## [1] "tabby"        "ChairmanMeow" "FuzzAldrin"
```

``` r
#Identifies and stores all of the unique cat colours contained in the data frame
cat_colours = unique(cat_data$colour)

#For all values of c between 1 and the length of the cat_colours vector 
#(i.e. - the number of different unique colours)
for(c in 1:length(cat_colours)){
  #Subset the data to include just one of colours 
  #(specified as position c in the cat_colour vector)
  subset = cat_data[cat_data$colour == cat_colours[c],]
  #From that subset, print the colour in question and all the names of cats of that colour 
  print(c(cat_colours[c], subset$name))
}
## [1] "black"      "MrWhiskers" "UmaPurrman"
## [1] "orange"     "CatStevens"
## [1] "tabby"        "ChairmanMeow" "FuzzAldrin"
```

There are endless ways to use a “for loop” in data analysis and
manipulation, limited only by your creativity. Some of the more common
modifications to a “for loop” are illustrated below.

## Modifying the for statement

For statements are fairly flexible, despite (or maybe because of) their
simplicity. You can use any variable name, for example. You can also
modify the values the variable will take on - this component of the for
statement is essentially just a vector of values; any vector can be used
to determine the variable values the loop will cycle through.

``` r
for(variable in 3:7){
  print(variable)
}
## [1] 3
## [1] 4
## [1] 5
## [1] 6
## [1] 7
```

``` r
for(a in seq(from = 3, to = 10, by = 2)){
  print(a)
}
## [1] 3
## [1] 5
## [1] 7
## [1] 9
```

``` r
sentence = c("this", "vector", "contains", "text")
for(word in sentence){
  print(word)
}
## [1] "this"
## [1] "vector"
## [1] "contains"
## [1] "text"
```

### The counter

In some cases, you’ll want to keep track of how many iterations you’ve
gone through, or the sum of values you’ve processed. To do this, we use
a code object called a counter. Remember, each iteration is independent
of the others - Any variables you assign **inside** the code chunk get
reset at the beginning of the next iteration when the “for loop” runs
the code chunk again. To keep track of the number of iterations or the
sum of values though, you need to retain this information somehow. To
get around this, you set the variable’s initial value **before** the
“for loop”. Compare the output of the two examples below. Why are they
producing different outputs?

``` r
for(i in 1:10){
  a = 0
  a = a + i
  print(a)
}
## [1] 1
## [1] 2
## [1] 3
## [1] 4
## [1] 5
## [1] 6
## [1] 7
## [1] 8
## [1] 9
## [1] 10
```

``` r
b = 0
for(i in 1:10){
  b = b + i
  print(b)
}
## [1] 1
## [1] 3
## [1] 6
## [1] 10
## [1] 15
## [1] 21
## [1] 28
## [1] 36
## [1] 45
## [1] 55
```

The second example sums up all the values of i used in the “for loop”,
using this counter object to “protect” the value from the iterative
resets. Counters, as their name implies, are also used to count
iterations. In the example below, the value of the counter goes up by
one during each iteration. After the “for loop” has run through all of
its iterations, printing the counter confirms that there were 10
iterations run.

``` r
counter = 0
for(i in 1:10){
  counter = counter + 1
}

print(counter)
## [1] 10

#note that in this specific instance the same 
#information can be retrieved by printing i
print(i)
## [1] 10
```

In this simple case, you can get the same information by printing the
variable ‘i’, but these counters can be useful as you get into more
complex “for loop” structures. For example, what happens if we have a
**nested for loop**? This refers to a “for loop” inside a “for loop”.
For every individual iteration of the outside loop, the inside loop runs
to completion.

``` r
counter = 0
for(i in 1:3){
  for(j in 1:4){
    print(c(i,j))
    counter = counter + 1
  }
}
## [1] 1 1
## [1] 1 2
## [1] 1 3
## [1] 1 4
## [1] 2 1
## [1] 2 2
## [1] 2 3
## [1] 2 4
## [1] 3 1
## [1] 3 2
## [1] 3 3
## [1] 3 4

print(c(i, j, counter))
## [1]  3  4 12
```

In this case, the number of iterations is different from the final
values of either of the two variables. You can still simply take the
product of the two final variable values to get the number of
iterations, but in many cases, more complex “for loops” have maximum
variable values that change across iterations, making this much more
difficult. In those cases, the counter structure is the best option. Can
you think of one of the weaknesses of a counter structure? What happens
if you run the “for loop” multiple times without resetting the counter?

Counters are also commonly used to count the occurrence of specific
types or values of data (often referred to as a ‘flag’ instead of a
counter in these cases). Again, oftentimes this data can be retrieved
using something like table() or a logical subset, but as you get into
more complex analyses and code, running a flag within or alongside
another process can sometimes be useful.

``` r
tabbies = 0
for(i in 1:length(cat_data$colour)){
  if(cat_data$colour[i] == "tabby"){
    tabbies = tabbies + 1
  }
}

print(tabbies)
## [1] 2
```

The above example also introduces the final code structure we’ll be
covering in this portion of the tutorial: the if / else statement.

# If / Else statements

Much like the “for loop”, if / else statements are a technique to help
automate or simplify coding. If / else statements rely on the
fulfillment of a logical statement to determine what to do. Because
these statements have two outcomes (True or False), these statements are
essentially ways to encode binary decision making into your analysis.

``` r
#For all values of j between 1 and 7...
for(j in 1:7){
  
  #if the value of j is equal to 5...
  if(j == 5){
    #then print the value of j
    print(j)
    #otherwise...
  }else{
    #print this message
    print("this value does not equal 5")
  }
}
## [1] "this value does not equal 5"
## [1] "this value does not equal 5"
## [1] "this value does not equal 5"
## [1] "this value does not equal 5"
## [1] 5
## [1] "this value does not equal 5"
## [1] "this value does not equal 5"
```

If you don’t provide an alternative code using the else{} component, R
will continue on without doing anything.

``` r
#For all values of j between 1 and 10...
for(j in 1:10){
  
  #if the value of j is equal to 5...
  if(j == 5){
    #then print the value of j
    print(j)
  }
}
## [1] 5
```

As with “for loops”, if / else statements can be used in many ways
during analyses. Understanding the basic syntax of these more complex
coding structures should be enough for you to modify them to fit your
needs.

# While Statements

Both for loops and if/else statements tend to be fairly concrete in
terms of number of iterations or operations. But what can you do if you
want to run an operation until a certain condition is satisfied? Without
knowing ahead of time how many operations are needed, a for loop may not
be useful or efficient. An if/else statement will do different things
based on the current status, but won’t reiterate automatically. The
while statement allows you to set a condition, and then run a chunk of
code until that condition is satisfied. Be careful, however, to ensure
that the code chunk will eventually satisfy the stated condition,
otherwise the while statement will keep running forever.

``` r
c = 1 
while(c < 10){
  print(paste("c is equal to ", c,". ", "This values of c is still too small", sep = ""))
  c = c + 1
  #d = d + 1    Replacing the above line with this would result in a while statement that runs forever.
}
## [1] "c is equal to 1. This values of c is still too small"
## [1] "c is equal to 2. This values of c is still too small"
## [1] "c is equal to 3. This values of c is still too small"
## [1] "c is equal to 4. This values of c is still too small"
## [1] "c is equal to 5. This values of c is still too small"
## [1] "c is equal to 6. This values of c is still too small"
## [1] "c is equal to 7. This values of c is still too small"
## [1] "c is equal to 8. This values of c is still too small"
## [1] "c is equal to 9. This values of c is still too small"
```

A simple manual solution is to set limits on the number of iterations
the while statement will run. This can be done using the counter objects
we described above. In the example below, the operation stops after 100
iterations, even if the main condition (that c exceeds 10) is not met.

``` r
c = 1 
d = 1
counter = 0

while(c < 10 & counter < 100){
  d = d + 1
  counter = counter + 1
}

print(counter)
## [1] 100
```

This is the end of the second tutorial. We have covered a lot of the
basics of using R to manipulate and examine data. You should now be able
to import data from an external file, examine the structure of the data,
describe basic qualities (like the mean and maximum values), and subset
the data. Using “for loops”, if/else statements, and while statements,
you should also be able to start piecing together more complex processes
These are the fundamental building blocks to performing analyses in R.
Much of this uses “Base R” - the collection of functions and
capabilities that come pre-loaded. As we move through the remaining
tutorials, we will supplement (and sometimes replace) what we have
already covered with more streamlined, sophisticated, or useful
techniques and functions. As with any skill though, you should master
the basics first.
