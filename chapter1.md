---
title       : Getting Started With Plotly
description : This chapter will introduce you to plotly and how you can use R and plotly together to create stunning data visualizations

--- type:NormalExercise lang:r xp:100 skills:1 key:7dc7c83d61
## Let's get started

[Plotly](https://plot.ly/) allows anyone to make beautiful, interactive web-based graphs. 

In this short tutorial, you'll be introduced to the [R package for plotly](https://www.rdocumentation.org/packages/plotly/versions/4.5.2?), a high-level interface to the open source JavaScript graphing library plotly.js. Plotly for R runs locally in your web browser or in the R Studio viewer. You can publish your charts to the web with [plotly's web service](https://plot.ly/r/getting-started).

Let's get started by loading the `plotly` library. 

*** =instructions
- Load the `plotly` library
- Click Submit Answer to run the code

*** =hint
- Use the `library()` function to load the plotly R package

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# load the `plotly` library


# This will create your very first plotly visualization
plot_ly(z = ~volcano)

```

*** =solution
```{r}
# load the `plotly` library
library(plotly)

# This will create your very first plotly visualization
plot_ly(z = ~volcano)

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
test_function("library", args = "x")

test_error()

success_msg("This was easy. Let's get some serious work done.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:804e39053c
## Diamonds are forever: a scatterplot

We'll use several datasets throughout the tutorial to showcase the power of plotly. In the next exercises we will make use of the `diamond` dataset, a dataset containing the prices and other attributes of 1000 diamonds. You're encouraged to think about how the examples can be applied to your own data-sets!

Plotly graphs are interactive. So make sure to experiment a bit with your plot: click-drag to zoom, shift-click to pan, double-click to autoscale.

*** =instructions
- plotly has already been loaded for you. Take a look at the first command. It plots the carat (weight of the diamond) against the price (in US dollars). You don't have to change anything about this command.
- In the second call of plot.ly() change the color argument in aes() (which stands for aesthetics). The color should be dependent on the weight of the diamond.
- In the third call of plot.ly() change the size argument in aes() (which stands for aesthetics). The size should be dependent on the weight of the diamond.

*** =hint
- The second argument of the second plot.ly() should contain argument `color` set to `carat`. 

*** =pre_exercise_code
```{r}
library(plotly)
library(ggplot2)
diamonds <- diamonds[sample(nrow(diamonds), 1000), ]
```

*** =sample_code
```{r}
# The diamonds data set
str(diamonds)

# A firs scatterplot has been made for you
plot_ly(diamonds, x = ~carat, y = ~price)

# Replace ___ with the correct vector
plot_ly(diamonds, x = ~carat, y = ~price, color = ~___)
        
# Replace ___ with the correct vector
plot_ly(diamonds, x = ~carat, y = ~price, color = ~___,
        size = ~___)
```

*** =solution
```{r}
# The diamonds data set
str(diamonds)

# A firs scatterplot has been made for you
plot_ly(diamonds, x = ~carat, y = ~price)

# Replace ___ with the correct vector
plot_ly(diamonds, x = ~carat, y = ~price, color = ~carat)
        
# Replace ___ with the correct vector
plot_ly(diamonds, x = ~carat, y = ~price, color = ~carat,
        size = ~carat)
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
test_function("library", args = "x")

test_error()

success_msg("This was easy. Let's get some serious work done.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:97ba0a444c
## The Interactive Bar Chart

You've likely encountered a bar chart before. With plotly you can now turn your basic bar charts into interactive masterpieces!

You will work again with the `diamonds` dataset. The goal is to create a bar chart that buckets our diamonds based on quality of the `cut`. Next, for each cut, we want to see how many diamonds there are for each `clarity`.  

Exciting!

*** =instructions
- Calculate the number of diamonds for each cut<->clarity combination. Do this using the `count` function in the [`dplyr`](https://www.rdocumentation.org/packages/dplyr/versions/0.5.0) package and assign the result to `diamonds_bucket`. 
- Next, create a chart of type "bar". The color should dependent on the clarity of the diamond while the x-axis should bucket your diamonds by the cut. 
- Plotly and dplyr are already loaded in. 

*** =hint
- You can calculate the numbers of diamonds for each cut<->clarity using `count(cut, clarity)`. (Not familiar with dplyr? Check [our course](https://www.datacamp.com/courses/dplyr-data-manipulation-r-tutorial)).
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
plot_ly(diamonds_bucket, x = ___, y = ~n, type= ___, color = ___) 

```

*** =solution
```{r}

# Calculate the numbers of diamonds for each cut<->clarity combination
diamonds_bucket <- diamonds %>% count(cut, clarity)

# Replace ___ with the correct vector
plot_ly(diamonds_bucket, x = ~cut, y = ~n, type= "bar", color = ~clarity) 

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
test_function("library", args = "x")

test_error()

success_msg("This was easy. Let's get some serious work done.")
```
--- type:NormalExercise lang:r xp:100 skills:1 key:126082cf3d
## The Interactive Box Plot

In the final exercise of this chapter you will make an interactive box plot in R. Using plotly, you can create box plots that are grouped, colored, and that display the underlying data distribution.

The code to create a simple box plot with plotly is provided in the code on your right. Note how you use `type= "box"` in the function `plot_ly` to create a box plot. Make sure to run the code. 
 

Exciting!

*** =instructions
- Create a second, more fancy, box plot using `diamonds`. The y-axis should represent the `price`. The color should depend on the `cut`.
- Create a third box plot where you bucket the diamonds not only by `cut` but also by `clarity`. The color should depend on the `clarity` of the diamond.  
- Plotly is already loaded in. 

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
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
test_function("library", args = "x")

test_error()

success_msg("This was easy. Let's get some serious work done.")
```
