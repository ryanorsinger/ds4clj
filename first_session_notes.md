# DS4CLJ Meeting Notes

## Our R Textbook
- [R for Data Science](https://r4ds.had.co.nz/)

## News
Hadley Wickham and publishers have given permission to Daniel (or the SciCloj group, perhaps) to make a Clojure version of this book.

## How to pull up the documentation
`?functionname` like `?print` or `?abs`, for example

## Recommendations
- Run `library(tidyverse)` nice and early.

## How to do things
- Make a vector `c(1, 13, -3)`, this is an atomic vector. `c` function is for "combine"
- `class(3:22)` tells us the data type. This is more common than using `typeof`
- 'All elements are of the same type'
- `rnorm(9)` creates 9 random numbers w/ a normal distribution 0-1
- Everything is a vector, `9` is a vector. `c(1, 2, 3)` is a vector.
- In R, all our primitives are vectors
- Many functions in R respect that anything is a vector and a vector could be longer than 1
- Primitives are also vectors (atomic, homogeneous vectors)
- Lists can have heterogenous types, different data types like list(2, "bob", TRUE, "Bob"). Lists are NOT atomic vectors
- Since atomic vectors are all the same type, then there's a heigharchy of type conversion
    - `c(1, "bob")` produces the vector "1" "bob"
    - `c(TRUE, "Janet")
- Dataframes are our data structure for tabular data, Try this: `data.frame(x=c(1, 3, 5), y=c(T, F, T))`
- Variable assignment `x <- 5` or `df = data.frame(x=c(1, 3, 5), y=c(T, F, T))`
- Dataframe access syntax:
  - df[1] returns the first row (1 indexed, not zero indexed)
  - df["x"] returns the "x" column
  - `as.list(df)` converts a dataframe into a list (and we see it's a list of atomic vectors)
  - A dataframe is essentially a list of columns, a list of vectors
- Lambda/anonymous function syntax is `f <- function(x) x*2` or `g <- function(x) x + 9`
- The `%>%` Pipe Operator is similar to `->` threading macro in Clojure, this comes when you use `library(tidyverse)
- Consider `5 %>% f %> g` to read/evaluate function pipelines from left to right.
- `attributes(df)` tells us about that object's attributes
- How to see documentation for a function, type `?functioname`, like `?c` or `?print` or `?abs`, for example.

## Visuals
- Run`data(mpg)` to load up a starter dataframe
- Run `ggplot(data = mpg) + geom_point((mapping = aes(x = displ, y=hwy)))` to visualize

##  Working with a Dataframe
- `data(mpg)` loads the mpg dataset into memory, globally
- `class(mpg)` shows the data type
- `attributes(mpg)` outputs the different attribute information about that dataframe
- `mpg %>% select(manufacturer, model, year)` is `select(mpg, manufacturer, model, year)`
- `mpg %>% select(manufacturer, model, year) %>% mutate(age = 2022 - year)`
- and we can assign the transformed output like this:
  - `x <- mpg %>% select(manufacturer, model, year) %>% mutate(age = 2022 - year)` binds the new dataframe to `x`

## Group By and Summarize
```
mpg %>% 
  select(manufacturer, model, year, cyl) %>% 
  group_by(manufacturer) %>%
  summarise(avg_year = mean(year))
```

- In the next example, the `n()` part is the number of rows per group (manufacturer). Think of this compared to COUNT when used in a SQL groupby

```
mpg %>% 
  select(manufacturer, model, year, cyl) %>% 
  group_by(manufacturer) %>%
  summarise(avg_year = mean(year),
    num_of_models=length(unique(model)),
    num_of_cars = n())
```

## Key Idea of "Tidy Data"
- Tidy Data = each row is an obervation and each variable/property is a column and cells are values.
- Principle of long vs. wide data. Consider having a spreadsheet where there is a year number for every column. A tidy approach would be a "year" column with the year's value in the cell.
- For more on Tidy Data principles, see [https://vita.had.co.nz/papers/tidy-data.pdf](https://vita.had.co.nz/papers/tidy-data.pdf)

## Using `With`. Consider the following
- Setup `l1 = list(x=c(3, 1, 9), y=1000)` in memory
- If we try to operate on `y` globally, that's not bound.
- But we can run `with(l1, y*2.3)` to bind and operate on that y value


## Comparing with Clojure
- Clojure core does not natively provide "everything is a vector", but there is the library called `dtype-next` that implements/offers arrays/buffers that work like these R vectors.
- Tablecloth

## Thanks
- Thanks to everyone who could join today!
- Special thanks to Daniel for organizing this group and running today's session!