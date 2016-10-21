---
title       : Getting Fancy With Plotly
description : In this chapter you will bring your plotly skills to the next level. Learn how to use plotly to create heatmaps and 3D surface plots, a choropleth map, and how to add slides. There is even a short meet and greet with ggplotly, the interactive sister of ggplot2. 

--- type:NormalExercise lang:r xp:100 skills:1 key:7dc7c83d61
## Visualizing volcano data

Mount Eden is a volcano in the Auckland volcanic field. The [`volcano`](https://www.rdocumentation.org/packages/datasets/versions/3.3.1/topics/volcano) dataset gives topographic information for Mount Eden on a 10m by 10m grid. Run `str(volcano)` to examine the dataset. 

<center><img src="http://lh6.ggpht.com/-ONlugp32B3o/VHwNdsi3EcI/AAAAAAAA9dI/b9DWnqncHFA/mount-wellington%25255B5%25255D.jpg?imgmax=800"; height="200px"</center>
<br><br></center>

One way to look at the topographic data is via a heatmap. The heatmap's color pattern visualizes how the height of the volcano's surface fluctuates within this 10m by 10m grid. 

Alternatively, you could visualize the data by making a 3D surface plot. Namely, plotly visualizations don't actually require a data frame. This makes chart types that accept a `z` argument especially easy to use if you have a numeric matrix such as our `volcano` dataset.  

Let's try to create that heatmap and 3D surface plot.

*** =instructions
Create two interactive plots using the volcano dataset:

- For one the `type` of trace is a `heatmap`.
- For the other `surface` since you also want to see a 3D representation.

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
plot_ly(z = ~volcano, type = "heatmap")

# The 3d surface map
plot_ly(z = ~volcano, type = "surface")

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

# Test library plotly 
test_library_function("plotly")
msg <- "You don't have to change the [`plot_ly`](https://www.rdocumentation.org/packages/plotly/versions/4.5.2/topics/plotly) command, it was predefined for you."
test_function("plot_ly", args = "z", index = 1, incorrect_msg = msg)

# Test str function
msg <-  "Call [`str()`](http://www.rdocumentation.org/packages/utils/functions/str) with the `volcano` dataset as an argument."
test_function("str", "object", not_called_msg = msg, incorrect_msg = msg)

# Test heatmap
test_function("plot_ly", args = c("z","type"),
              not_called_msg = "Have you used `plot_ly()` 2 times for 2 different graphs?",
              index = 1,
              args_not_specified = c("Have you correctly specified that `z` should be `volcano`?",
                                "Have you correctly specified that `type` should be `heatmap`?"),
              incorrect_msg = c("Have you correctly specified that `z` should be `volcano`?",
                                "Have you correctly specified that `type` should be `heatmap`?"))

# Test 3d surface map
test_function("plot_ly", args = c("z","type"),
              not_called_msg = "Have you used `plot_ly()` 2 times for 2 different graphs?",
              index = 2,
              args_not_specified = c("Have you correctly specified that `z` should be `volcano`?",
                                "Have you correctly specified that `type` should be `surface`?"),
              incorrect_msg = c("Have you correctly specified that `z` should be `volcano`?",
                                "Have you correctly specified that `type` should be `surface`?"))
                                
                                
success_msg("Congratz! You created your very first heatmap and 3D surface map.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:15071c2604
## ggplot2, the interactive dimension

[`ggplot2`](https://www.rdocumentation.org/packages/ggplot2/versions/2.1.0) is probably one of the most well known graphing libraries for R. With [`ggplotly()`](https://www.rdocumentation.org/packages/plotly/versions/4.5.2/topics/ggplotly) from plotly, you can now convert your ggplot2 plots into interactive, web-based versions. See [these examples](https://plot.ly/ggplot2/) on how ggplotly does in converting different ggplot2 examples. 

Let's try it yourself. 

Converting a ggplot2 chart to an interactive chart is fairly easy. First you create the ggplot2 graph and next you call `ggplotly()`. Like this:

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

# Test ggplot2
test_function("ggplot", args = "data")
test_function("aes", args = c("x", "y", "col"), eval = c(F, F, F))
test_function("geom_point")

# Test ggplotly
test_function("ggplotly")

success_msg("You successfully turned a static ggplot2 graph into an interactive ggplot2 graph. Woot Woot!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:dc9f2c11f7
## An interactive world map

Ever wonder how some data scientists make these beautiful geographical maps? This exercise shows you how they do it.

A choropleth map provides an easy way to visualize how a measurement varies across a geographic area or it shows the level of variability within a region. An example of such a map is provided on the right. Run the code and you will see a map of the USA showing the 2011 US Agriculture Exports by State. Hover over each state to see the export value per state in Millions USD. 

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
library(plotly)
library(choroplethr)
library(ggplot2)
library(dplyr)
us_ag_exports = read.csv('http://s3.amazonaws.com/assets.datacamp.com/course/plotly/US_AG_EXPORTS.csv')
us_ag_exports = us_ag_exports[,c(2,5)]

world_gdp_2014 = read.csv('http://s3.amazonaws.com/assets.datacamp.com/course/plotly/GDP_WORLD.csv')
world_gdp_2014 = world_gdp_2014[,3:4]

```

*** =sample_code
```{r}

# US Agriculture Exports
plot_ly(type="choropleth",locations = us_ag_exports$code, locationmode="USA-states",color = us_ag_exports$total.exports, colors = 'Reds', z = us_ag_exports$total.exports) %>% layout(geo = list(scope = 'usa'), title = "2011 US Agriculture Exports by State")

# 2014 global GDP
str(world_gdp_2014)

# 2014 Global GDP
plot_ly(___,___, ____,
        color = world_gdp_2014$GDP..BILLIONS, colors = 'Blues', ___) %>% 
  ___(___ = "2014 Global GDP") 
  
```

*** =solution
```{r}

# US Agriculture Exports
plot_ly(type="choropleth",locations = us_ag_exports$code, locationmode="USA-states",color = us_ag_exports$total.exports, colors = 'Reds', z = us_ag_exports$total.exports) %>% layout(geo = list(scope = 'usa'), title = "2011 US Agriculture Exports by State")


# 2014 global GDP
str(world_gdp_2014)

# 2014 Global GDP
plot_ly(type="choropleth",locations = world_gdp_2014$CODE, locationmode="g",
        color = world_gdp_2014$GDP..BILLIONS, colors = 'Blues', z = world_gdp_2014$GDP..BILLIONS) %>% 
  layout(title = "2014 Global GDP")

```

*** =sct
```{r}

# Test 2014 global gdp
test_function("plot_ly", args = c("type","locations","locationmode","color","colors","z"), 
              not_called_msg = "Have you used `plot_ly()` 2 times for 2 different graphs?",
              index = 2,
              args_not_specified = c("Have you correctly specified that `type` should be `choropleth`?",
                                "Have you correctly specified that `locations` should be `us_ag_exports$code`?",
                                "Have you correctly specified that `locationmode` should be `USA-states`?",
                                "Have you correctly specified that `color` should be `us_ag_exports$total.exports`?",
                                "Have you correctly specified that `colors` should be `Reds`?",
                                "Have you correctly specified that `z` should be `us_ag_exports$total.exports`?"),
              incorrect_msg = c("Have you correctly specified that `type` should be `choropleth`?",
                                "Have you correctly specified that `locations` should be `us_ag_exports$code`?",
                                "Have you correctly specified that `locationmode` should be `USA-states`?",
                                "Have you correctly specified that `color` should be `us_ag_exports$total.exports`?",
                                "Have you correctly specified that `colors` should be `Reds`?",
                                "Have you correctly specified that `z` should be `us_ag_exports$total.exports`?"))


test_function("layout",args = c("geo","title"),index = 1)


# Test str function
msg <-  "Call [`str()`](http://www.rdocumentation.org/packages/utils/functions/str) with the `world_gdp_2014` dataset as an argument."
test_function("str", "object", not_called_msg = msg, incorrect_msg = msg)

# Test 2014 global gdp
test_function("plot_ly", args = c("type","locations","locationmode","color","colors","z"), 
              not_called_msg = "Have you used `plot_ly()` 2 times for 2 different graphs?",
              index = 2,
              args_not_specified = c("Have you correctly specified that `type` should be `choropleth`?",
                                "Have you correctly specified that `locations` should be `world_gdp_2014$CODE`?",
                                "Have you correctly specified that `locationmode` should be `g`?",
                                "Have you correctly specified that `color` should be `world_gdp_2014$GDP..BILLIONS`?",
                                "Have you correctly specified that `colors` should be `Blues`?",
                                "Have you correctly specified that `z` should be `world_gdp_2014$GDP..BILLIONS`?"),
              incorrect_msg = c("Have you correctly specified that `type` should be `choropleth`?",
                                "Have you correctly specified that `locations` should be `world_gdp_2014$CODE`?",
                                "Have you correctly specified that `locationmode` should be `g`?",
                                "Have you correctly specified that `color` should be `world_gdp_2014$GDP..BILLIONS`?",
                                "Have you correctly specified that `colors` should be `Blues`?",
                                "Have you correctly specified that `z` should be `world_gdp_2014$GDP..BILLIONS`?"))

test_function("layout",args = c("title"),index = 2)

```

--- type:NormalExercise lang:r xp:100 skills:1 key:8e8d273075
## Sliding into the final exercise

For the final exercise in this course you will implement a range slider to a stock graph. 

On the right you see a plotly graph to which a range slider is added using `rangeslider()`. The plot looks at a time series `USAccDeaths` that gives the monthly totals of accidental deaths in the USA. Make sure to run the code in your console. 

Loaded in, you will find a dataset on Apple's stock price: `apple_stock_price`. Let's now visualize this stock price over time using an interactive plotly chart. Make sure to add a range slider.  

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

# First Plotly graph
test_function("plot_ly", args = c("x","y"),index = 1, args_not_specified = c("Have you correctly specified that `x` should be `time(USAccDeaths)`?",
                                "Have you correctly specified that `y` should be `USAccDeaths`?"), incorrect_msg = c("Have you correctly specified that `x` should be `time(USAccDeaths)`?","Have you correctly specified that `y` should be `USAccDeaths`?"))

test_function("add_lines",index = 1)
test_function("rangeslider",index = 1)

# Test str function
msg <-  "Call [`str()`](http://www.rdocumentation.org/packages/utils/functions/str) with the `apple_stock_price` dataset as an argument."
test_function("str", "object", not_called_msg = msg, incorrect_msg = msg)


# Second Plotly graph
test_function("plot_ly", args = c("data","x"),index = 2, args_not_specified = c("Have you correctly specified that `data` should be `apple_stock_price`?",
                                "Have you correctly specified that `x` should be `Date`?"), incorrect_msg = c("Have you correctly specified that `data` should be `apple_stock_price`?","Have you correctly specified that `x` should be `Date`?"))

test_function("add_lines",args = c("y","name"), index = 2, args_not_specified = c("Have you correctly specified that `y` should be `AAPL.Adjusted`?",
                                "Have you correctly specified that `name` should be `Apple`?"))

test_function("rangeslider",index = 2)

test_function("layout",args = c("title","xaxis","yaxis"), args_not_specified = c("Have you correctly specified that `title` should be `Stock Price     Apple`?","Have you correctly specified that `xaxis` should be `list(title = \"Date\")`?","Have you correctly specified that `yaxis` should be `list(title = \"Price\")`?"))

```
