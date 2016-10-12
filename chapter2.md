---
title       : Getting Fancy With Plotly
description : In this chapter we will bring your plotly skills to the next level. Here you will learn how to use plotly to create heatmaps and 3D surface plots, a choropleth map and we introduce you to ggplotly, the interactive sister of ggplot2. 

--- type:NormalExercise lang:r xp:100 skills:1 key:7dc7c83d61
## Visualizing volcano data

Mount Eden is a volcano in the Auckland volcanic field. The `volcano` dataset gives topographic information for Mount Eden on a 10m by 10m grid. Run `str(volcano)` to examine the dataset. 

One way to look at this data is by using a heatmap. The heatmap's color pattern then visualizes how the height of the volcano's surface fluctuates within this 10m by 10m grid. 

You could also visualize the data by making a 3D surface plot. How? Well, plotly visualizations don't actually require a data frame. This makes chart types that accept a z argument especially easy to use if you have a numeric matrix such as our `volcano` dataset.  

Like in the previous chapter, `plot_ly()` takes an argument `type`. Here you specify the type of trace. Let's try to create that heatmap and 3D surface plot.

*** =instructions
- Create two interactive plots using the volcano data set. For one the type of trace is a `heatmap` and for the other `surface`. 

*** =hint
- Remember: for both plots you need to specify the z argument.

*** =pre_exercise_code
```{r}
library(plotly)

```

*** =sample_code
```{r}
# Load the `plotly` library
library(plotly)

# Your volcano data
str(volcano)

# The heatmap
plot_ly(___ = ___, type = ___)

# The 3d surface map
plot_ly(___ = ___, type = ___)

```

*** =solution
```{r}
# Load the `plotly` library
library(plotly)

# Your volcano data
str(volcano)

# The heatmap
plot_ly(z = volcano, type = "heatmap")

# The 3d surface map
plot_ly(z = ~volcano, type = "surface")

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
test_function("library", args = "x")

test_error()

success_msg("This was easy. Let's get some serious work done.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:15071c2604
## Create interactive, online ggplot2 charts

ggplot2 is probably one of the most well known graphing library's for R and thanks to plotly you can now convert your ggplot2 plots to an interactive, web-based version using `ggplotly()`. See [these examples](https://plot.ly/ggplot2/ ) to see more examples on how ggplotly does in converting different ggplot2 examples. 

Let's try it yourself. Converting a ggplot2 chart to an interactive chart is fairly easy. First you create the ggplot2 graph and next you call `ggplotly()` like this:

`my_ggplot2 = qplot(carat, price, data=diamonds, colour=clarity)
ggplotly(my_ggplot2)`

Not yet familiar with the ggplot2 syntax? [Consider taking this interactive tutorial](https://www.datacamp.com/courses/data-visualization-with-ggplot2-1).

*** =instructions
The `mtcars` data frame is available in your workspace. Use `geom_point()` for your plot:
- Using ggplot2, map wt onto the x aesthetic, mpg onto the y aesthetic, and cyl onto color. 
- Use `ggplotly()` to make your plot interactive 


*** =hint
- Remember: for both plots you need to specify the z argument.

*** =pre_exercise_code
```{r}
library(plotly)
library(ggplot2)
diamonds <- diamonds[sample(nrow(diamonds), 1000), ]

```

*** =sample_code
```{r}

# Create the ggplot2 graph
ggplot(___, aes(x = ___, y = ___, col = ___)) +
  geom_point()

# Make your plot interactive


```

*** =solution
```{r}

# Create the ggplot2 graph
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl)) +
  geom_point()

# Make your plot interactive
ggplotly()

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
test_function("library", args = "x")

test_error()

success_msg("This was easy. Let's get some serious work done.")
```
