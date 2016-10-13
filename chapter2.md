---
title       : Getting Fancy With Plotly
description : In this chapter we will bring your plotly skills to the next level. Learn how to use plotly to create heatmaps and 3D surface plots, a choropleth map, and how to add slides. There is even a short meet and greet with ggplotly, the interactive sister of ggplot2. 

--- type:NormalExercise lang:r xp:100 skills:1 key:7dc7c83d61
## Visualizing volcano data

Mount Eden is a volcano in the Auckland volcanic field. The [`volcano`](https://www.rdocumentation.org/packages/datasets/versions/3.3.1/topics/volcano) dataset gives topographic information for Mount Eden on a 10m by 10m grid. Run `str(volcano)` to examine the dataset. 

<center><img src="http://lh6.ggpht.com/-ONlugp32B3o/VHwNdsi3EcI/AAAAAAAA9dI/b9DWnqncHFA/mount-wellington%25255B5%25255D.jpg?imgmax=800"; height="200px"</center>
<br><br></center>

One way to look at the topographic data is via a heatmap. The heatmap's color pattern visualizes how the height of the volcano's surface fluctuates within this 10m by 10m grid. 

Alternatively, you could visualize the data by making a 3D surface plot. Namely, plotly visualizations don't actually require a data frame. This makes chart types that accept a `z` argument especially easy to use if you have a numeric matrix such as our `volcano` dataset.  

Let's try to create that heatmap and 3D surface plot.

*** =instructions
Create two interactive plots using the volcano data set:

- For one the `type` of trace is a `heatmap`.
- For the other `surface` since we also want to see a 3D representation.

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
success_msg("This was easy. Let's get some serious work done.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:15071c2604
## ggplot2, the interactive dimension

[`ggplot2`](https://www.rdocumentation.org/packages/ggplot2/versions/2.1.0) is probably one of the most well known graphing library's for R. With [`ggplotly()`](https://www.rdocumentation.org/packages/plotly/versions/4.5.2/topics/ggplotly) from plotly you can now convert your ggplot2 plots into interactive, web-based versions. See [these examples](https://plot.ly/ggplot2/) on how ggplotly does in converting different ggplot2 examples. 

Let's try it yourself. Converting a ggplot2 chart to an interactive chart is fairly easy. First you create the ggplot2 graph and next you call `ggplotly()` like this:

<pre>
my_ggplot2 = qplot(carat, price, data = diamonds, 
                   colour = clarity)
ggplotly(my_ggplot2)</pre>


Not yet familiar with the ggplot2 syntax? [Consider taking this interactive tutorial](https://www.datacamp.com/courses/data-visualization-with-ggplot2-1).

*** =instructions
The `mtcars` data frame is available in your workspace. Use `geom_point()` for your plot:

- Using ggplot2, map `wt` onto the `x` aesthetic, `mpg` onto the `y` aesthetic, and `cyl` onto `color`. 
- Use `ggplotly()` to make your plot interactive. 


*** =hint
- You can make your plot interactive by adding `ggplotly()`

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
success_msg("This was easy. Let's get some serious work done.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:dc9f2c11f7
## An interactive world map

Ever wonder how some data scientists make these beautiful geographical maps? In this exercise we show you how they do it.

A choropleth map provides an easy way to visualize how a measurement varies across a geographic area or it shows the level of variability within a region. We provided an example of such a map on the right. Run the code and you will see a map of the USA showing the 2011 US Agriculture Exports by State. Hover over each state to see the export value per state in Millions USD. 

Let's highlight the most important pieces in the code:

- The `locations` argument sets the geographic locations corresponding to each value in `z`.  
- `locationmode` determines the set of locations used to match entries in `locations` to regions on the map. In this case `USA-states`.
- In `layout()` you modify the layout of a plotly visualization. With e.g. `geo` you tell plotly to only show the `usa` map (remove `geo` and you will have a map of the world). 


*** =instructions
- Based on the US Agriculture Exports choropleth map code, create a choropleth map showing the 2014 global GDP (`world_gdp_2014`) for each country.
- For a map of the world, the `locationmode` is `"g"`.

*** =hint
- To set the `locations` arguments use `locations = world_gdp_2014$CODE`.

*** =pre_exercise_code
```{r}
library(choroplethr)
library(ggplot2)
library(dplyr)
us_ag_exports = read.csv('http://raw.githubusercontent.com/plotly/datasets/master/2011_us_ag_exports.csv')
us_ag_exports = us_ag_exports[,c(1,4)]

world_gdp_2014 = read.csv('http://raw.githubusercontent.com/plotly/datasets/master/2014_world_gdp_with_codes.csv')
world_gdp_2014 = world_gdp_2014[,2:3]

```

*** =sample_code
```{r}

# US Agriculture Exports
plot_ly(type="choropleth",locations = us_ag_exports$code, locationmode="USA-states",color = us_ag_exports$total.exports, colors = 'Reds', z = us_ag_exports$total.exports) %>% layout(geo = list(scope = 'usa'), title = "2011 US Agriculture Exports by State") %>% colorbar(title="Millions USD")

# 2014 global GDP
str(world_gdp_2014)

# 2014 Global GDP
plot_ly(___,___, ____,
        color = world_gdp_2014$GDP..BILLIONS, colors = 'Blues', ___) %>% 
  ___(___ = "2014 Global GDP") %>% ___(___ = "GDP Billions US$")
  
```

*** =solution
```{r}

# US Agriculture Exports
plot_ly(type="choropleth",locations = us_ag_exports$code, locationmode="USA-states",
        color = us_ag_exports$total.exports, colors = 'Reds', z = us_ag_exports$total.exports) %>% 
  layout(geo = list(scope = 'usa'), title = "2011 US Agriculture Exports by State") %>% colorbar(title="Millions USD")


# 2014 global GDP
str(world_gdp_2014)

# 2014 Global GDP
plot_ly(type="choropleth",locations = world_gdp_2014$CODE, locationmode="g",
        color = world_gdp_2014$GDP..BILLIONS, colors = 'Blues', z = world_gdp_2014$GDP..BILLIONS) %>% 
  layout(title = "2014 Global GDP") %>% colorbar(title="GDP Billions US$")

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
success_msg("This was easy. Let's get some serious work done.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:8e8d273075
## Sliding into the final exercise

For the final exercise in this course you will implement a range slider to a stock graph. 

On the right you see a plotly graph to which a range slider is added using `rangeslider()`. The plot looks at a time series `USAccDeaths` that gives the monthly totals of accidental deaths in the USA. Make sure to run the code. 

Loaded in, you will find a data set on Apple's stock price: `apple_stock_price`. Let's now visualize this stock price over time using an interactive plotly chart. Make sure to add a range slider.  

*** =instructions
- Chart Apple's time-series data in R using `apple_stock_price`. Use the provided sample code.
- Make sure to add a range slider

*** =hint
- Not sure how to add a range slider? Type `?rangeslider` in the console. 

*** =pre_exercise_code
```{r}
library(plotly)
library(quantmod)

getSymbols(Symbols = c("AAPL"))
apple_stock_price <- data.frame(Date = index(AAPL), AAPL[,6])

```

*** =sample_code
```{r}

# Monthly totals of accidental deaths in the USA
plot_ly(x = time(USAccDeaths), y = USAccDeaths) %>% 
  add_lines() %>%
  rangeslider()

# Apple Stock Price
str(apple_stock_price)


# Apple Stock Price With Rangeslider
plot_ly(___, x = ~___) %>%
  add_lines(y = ~___, name = "Apple") %>% 
  ___ %>% 
  layout(
    title = "Stock Price Apple",
    xaxis = list(title = "Date"),
    yaxis = list(title = "Price"))
    
```

*** =solution
```{r}

# Monthly totals of accidental deaths in the USA
plot_ly(x = time(USAccDeaths), y = USAccDeaths) %>% 
  add_lines() %>%
  rangeslider()

# Apple Stock Price
str(apple_stock_price)


# Apple Stock Price With Rangeslider
plot_ly(apple_stock_price, x = ~Date) %>%
  add_lines(y = ~AAPL.Adjusted, name = "Apple") %>% 
  rangeslider() %>% 
  layout(
    title = "Stock Price Apple",
    xaxis = list(title = "Date"),
    yaxis = list(title = "Price"))

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
success_msg("This was easy. Let's get some serious work done.")
```
