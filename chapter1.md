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
## The Single Bar Chart




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
