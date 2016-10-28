---
title       : Getting Started With Plotly
description : This chapter will introduce you to plotly and how you can use R and plotly together to create stunning data visualizations.

--- type:NormalExercise lang:r xp:100 skills:1 key:7dc7c83d61
## Let's get started

Meet Plotly. 

[Plotly](https://plot.ly/) provides online graphing, analytics, and statistics tools. Using their technology anyone, including yourself, can make beautiful, interactive web-based graphs.

In this short tutorial, you'll be introduced to the [R package for plotly](https://www.rdocumentation.org/packages/plotly/versions/4.5.2?), a high-level interface to the open source JavaScript graphing library plotly.js. 

Plotly for R runs locally in your web browser or in the R Studio viewer. You can publish your charts to the web with [plotly's web service](https://cpsievert.github.io/plotly_book/plot-ly-for-collaboration.html). 
Let's get started by loading the `plotly` library. 

*** =instructions
- Load the `plotly` R package.
- Click *Submit Answer* to run the code

*** =hint
- Use `library()` to load the plotly R package.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# load the `plotly` package


# This will create your very first plotly visualization
plot_ly(z = ~volcano)

```

*** =solution
```{r}
# load the `plotly` package
library(plotly)

# This will create your very first plotly visualization
plot_ly(z = ~volcano)

```

*** =sct
```{r}
test_library_function("plotly")

msg <- "You don't have to change the [`plot_ly`](https://www.rdocumentation.org/packages/plotly/versions/4.5.2/topics/plotly) command, it was predefined for you."
test_function("plot_ly", args = "z", index = 1, incorrect_msg = msg)

test_error()
success_msg("That was not that hard. Now it is time to create your very own plot.")

```

--- type:NormalExercise lang:r xp:100 skills:1 key:804e39053c
## Plotly diamonds are forever

You'll use several datasets throughout the tutorial to showcase the power of plotly. In the next exercises you will make use of the [`diamond`](https://www.rdocumentation.org/packages/ggplot2/versions/2.1.0/topics/diamonds) dataset. A dataset containing the prices and other attributes of 1000 diamonds. 

<center><img src="http://www.picgifs.com/glitter-gifs/d/diamonds/animaatjes-diamonds-61528.gif" alt="Diamonds" height="100px"></center>

Don't forget: 

You're encouraged to think about how the examples can be applied to your own data-sets! Also, Plotly graphs are interactive. So make sure to experiment a bit with your plot: click-drag to zoom, shift-click to pan, double-click to autoscale.

*** =instructions
- `plotly` has already been loaded for you. 
- Take a look at the first `plot_ly()` graph. It plots the `carat` (FYI: the carat is a unit of mass. Hence it gives info on the weight of a diamond,) against the `price` (in US dollars). You don't have to change anything to this command. Tip: note the `~` syntax. 
- In the second call of `plot_ly()`, change the `color` argument. The color should be dependent on the weight of the diamond.
- In the third call of `plot_ly()`, change the `size` argument as well. The size should be dependent on the weight of the diamond.

*** =hint
- The second argument of the second `plot_ly()` should contain argument `color` set to `carat`. 

*** =pre_exercise_code
```{r}
library(plotly)
library(ggplot2)
diamonds <- diamonds[sample(nrow(diamonds), 1000), ]
```

*** =sample_code
```{r}
# The diamonds dataset
str(diamonds)

# A firs scatterplot has been made for you
plot_ly(diamonds, x = ~carat, y = ~price)

# Replace ___ with the correct vector
plot_ly(diamonds, x = ~carat, y = ~price, color = ~___)
        
# Replace ___ with the correct vector
plot_ly(diamonds, x = ~carat, y = ~price, color = ~___, size = ~___)
```

*** =solution
```{r}
# The diamonds dataset
str(diamonds)

# A firs scatterplot has been made for you
plot_ly(diamonds, x = ~carat, y = ~price)

# Replace ___ with the correct vector
plot_ly(diamonds, x = ~carat, y = ~price, color = ~carat)
        
# Replace ___ with the correct vector
plot_ly(diamonds, x = ~carat, y = ~price, color = ~carat, size = ~carat)
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

# Test str function
msg <-  "Call [`str()`](http://www.rdocumentation.org/packages/utils/functions/str) with the `diamonds` dataset as an argument."
test_function("str", "object", not_called_msg = msg, incorrect_msg = msg)

# Test first plotly function
test_function("plot_ly", args = c("data","x","y"),
              not_called_msg = "Have you used `plot_ly()` 3 times for 3 different graphs?",
              index = 1,
              args_not_specified = c("Have you correctly specified that `data` should be `diamonds`?",
                                "Have you correctly specified that `x` should be `carat`?",
                                "Have you correctly specified that `y` should be `price`?"))

# Test second plotly function
test_function("plot_ly", args = c("data","x","y","color"),
              not_called_msg = "Have you used `plot_ly()` 3 times for 3 different graphs?",
              index = 2,
              args_not_specified = c("Have you correctly specified that `data` should be `diamonds`?",
                                "Have you correctly specified that `x` should be `carat`?",
                                "Have you correctly specified that `y` should be `price`?",
                                "Have you correctly specified that `color` should depend on `carat`?"))

# Test third plotly function
test_function("plot_ly", args = c("data","x","y","color","size"),
              not_called_msg = "Have you used `plot_ly()` 3 times for 3 different graphs?",
              index = 3,
              args_not_specified = c("Have you correctly specified that `data` should be `diamonds`?",
                                "Have you correctly specified that `x` should be `carat`?",
                                "Have you correctly specified that `y` should be `price`?",
                                "Have you correctly specified that `color` should depend on `carat`?",
                                "Have you correctly specified that `size` should depend on `carat`?"))
                                
success_msg("Wow. Those are some nice looking plots! You are a natural.")

```

--- type:NormalExercise lang:r xp:100 skills:1 key:97ba0a444c
## The interactive bar chart

You've likely encountered a bar chart before. With plotly you can now turn those dull, basic bar charts into interactive masterpieces!

You will work again with the `diamonds` dataset. The goal is to create a bar chart that buckets our diamonds based on quality of the `cut`. Next, for each cut, you want to see how many diamonds there are for each `clarity` variable.  

Exciting!

*** =instructions
- The `plotly` and `dplyr` package are already loaded in.
- Calculate the number of diamonds for each cut/clarity combination using the `count()` function from the [`dplyr`]((https://www.rdocumentation.org/packages/dplyr/versions/0.5.0)) package. Assign the result to `diamonds_bucket`. 
- Create a chart of type `"bar"`. The `color` of the bar depends on the `clarity` of the diamond. Bucket your diamonds by the `cut` over the x-axis. 


*** =hint
- Calculate the numbers of diamonds for each cut/clarity using `count(cut, clarity)`. (Not familiar with dplyr? Check [our course](https://www.datacamp.com/courses/dplyr-data-manipulation-r-tutorial)).
- Indicate you want a bar chart in plotly using `type= "bar"`

*** =pre_exercise_code
```{r}
library(plotly)
library(ggplot2)
library(dplyr)
diamonds <- diamonds[sample(nrow(diamonds), 1000), ]
```

*** =sample_code
```{r}

# Calculate the numbers of diamonds for each cut<->clarity combination
diamonds_bucket <- diamonds %>% count(___, ___)

# Replace ___ with the correct vector
plot_ly(diamonds_bucket, x = ___, y = ~n, type = ___, color = ___) 

```

*** =solution
```{r}

# Calculate the numbers of diamonds for each cut<->clarity combination
diamonds_bucket <- diamonds %>% count(cut, clarity)

# Replace ___ with the correct vector
plot_ly(diamonds_bucket, x = ~cut, y = ~n, type = "bar", color = ~clarity) 

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

# Test dplyr function
test_error()       

test_function_result("count", 
                     incorrect_msg = paste("Have you correctly performed the count operation?",
                                           "Make sure this is the `dplyr` verb you call on `diamonds`."))


# Test first plotly function
test_function("plot_ly", args = c("data","x","y","type","color"),
              not_called_msg = "Have you used `plot_ly()` to create a bar chart?",
              index = 1,
              args_not_specified = c("Have you correctly specified that `data` should be `diamonds_bucket`?",
                                "Have you correctly specified that `x` should be `cut`?",
                                "Have you correctly specified that `y` should be `n`?",
                                "Have you correctly specified that `type` should be `bar`?",
                                "Have you correctly specified that `color` should be `clarity`?"
                                ))
                                
success_msg("Well done. Time to move from the bar to the box...")

```
--- type:NormalExercise lang:r xp:100 skills:1 key:126082cf3d
## From the bar to the box: the box plot

In the final exercise of this chapter, you will make an interactive box plot in R. 

Using plotly, you can create box plots that are grouped, colored, and that display the underlying data distribution. The code to create a simple box plot using plotly is provided on your right. 

Note how you use `type= "box"` in the function `plot_ly()` to create a box plot. Make sure to run the code (`plotly` is already loaded in). 
 
*** =instructions
- Create a second, more fancy, box plot using `diamonds`. The y-axis should represent the `price`. The color should depend on the `cut`.
- Create a third box plot where you bucket the diamonds not only by `cut` but also by `clarity`. The color should depend on the `clarity` of the diamond.  


*** =hint
- For the third box plot the `x` argument should depend on the `cut`.

*** =pre_exercise_code
```{r}
library(plotly)
library(ggplot2)
library(dplyr)
diamonds <- diamonds[sample(nrow(diamonds), 1000), ]
```

*** =sample_code
```{r}

# The Non Fancy Box Plot
plot_ly(y = ~rnorm(50), type = "box")

# The Fancy Box Plot
plot_ly(diamonds, y = ___, color = ___, type = ___)

# The Super Fancy Box Plot
plot_ly(diamonds, x = ___, y = ___, color = ___, type = ___) %>%
  layout(boxmode = "group")
  
```

*** =solution
```{r}

# The Non Fancy Box Plot
plot_ly(y = ~rnorm(50), type = "box")

# The Fancy Box Plot
plot_ly(diamonds, y = ~price, color = ~cut, type = "box")

# The Super Fancy Box Plot
plot_ly(diamonds, x = ~cut, y = ~price, color = ~clarity, type = "box") %>%
  layout(boxmode = "group")
  
```

*** =sct
```{r}
# Test first plotly function
test_function("plot_ly", index = 1, args = c("y","type"), incorrect_msg = c("You don't have to change the [`plot_ly`](https://www.rdocumentation.org/packages/plotly/versions/4.5.2/topics/plotly) command, it was predefined for you.","You don't have to change the [`plot_ly`](https://www.rdocumentation.org/packages/plotly/versions/4.5.2/topics/plotly) command, it was predefined for you."))

# Test second plotly function
test_function("plot_ly", args = c("data","y","color","type"),
              not_called_msg = "Have you used `plot_ly()` 3 times for 3 different graphs?",
              index = 2,
              args_not_specified = c("Have you correctly specified that `data` should be `diamonds`?",
                                "Have you correctly specified that `y` should be `price`?",
                                "Have you correctly specified that `color` should depend on `cut`?",
                                "Make sure to let plotly know you need a plot of type box?"))
                                
# Test third plotly function
test_function("plot_ly", args = c("data","x","y","color","type"),
              not_called_msg = "Have you used `plot_ly()` 3 times for 3 different graphs?",
              index = 3,
              args_not_specified = c("Have you correctly specified that `data` should be `diamonds`?",
                                "Have you correctly specified that `x` should be `cut`?",
                                "Have you correctly specified that `y` should be `price`?",
                                "Have you correctly specified that `color` should depend on `clarity`?",
                                "Make sure to let plotly know you need a plot of type box?"))

test_function("layout", args = c("boxmode"),
                     incorrect_msg = paste("No need to change `layout()`!"))
                                           
success_msg("You really aced this chapter. Time to level up.")

```
