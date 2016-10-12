---
title       : Getting Fancy With Plotly
description : In this chapter we will bring your plotly skills to the next level. Here you will learn how to use plotly to create heatmaps and 3D surface plots, a choropleth map and we introduce you to ggplotly, the interactive sister of ggplot2. 

--- type:NormalExercise lang:r xp:100 skills:1 key:7dc7c83d61
## Visualizing volcano data

Mount Eden is a volcano in the Auckland volcanic field. The `volcano` dataset gives topographic information for Mount Eden on a 10m by 10m grid. Run `str(volcano)` to examine the dataset. 

One way to look at this data is by using a heatmap. The heatmap's color pattern then visualizes how the height of the volcano's surface fluctuates within this 10m by 10m grid. Another way for you is to visualize the data is by making a 3D surface plot. Namely, plotly visualizations don't actually require a data frame. This makes chart types that accept a z argument especially easy to use if you have a numeric matrix such as our `volcano` dataset. 

Like in the previous chapter, `plot_ly()` takes an argument `type`. Here you specify the type of trace. Let's try to create that heatmap and 3D surface plot.

*** =instructions
- Create two interactive plots using the volcano data set. For one the type of trace is a `heatmap` and for the other `surface`. 

*** =hint
- Remember: for both plots you need to specify the z argument.

*** =pre_exercise_code
```{r}
library(plotly)

#example plot
plot_ly(
  plotly::mic, r = ~r, t = ~t, color = ~nms, alpha = 0.5, type = "scatter"
)
layout(p, title = "Mic Patterns", orientation = -90)

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
