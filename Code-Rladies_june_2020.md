R-Ladies Mid-Mo: Plotting in R
================
Maggie Suero
10/6/2020

We are going to use the Palmer Penguins
[dataset](https://github.com/allisonhorst/palmerpenguins). The data were
collected and made available by Dr. Kristen Gorman and the Palmer
Station, Antarctica LTER.

Let’s start by knowing the penguins *(Artwork by @allison\_horst)*:

![Palmer
penguins](https://raw.githubusercontent.com/allisonhorst/palmerpenguins/master/man/figures/lter_penguins.png)

## Basic plot

``` r
p <- ggplot(data = penguins, aes(x = flipper_length_mm, y = body_mass_g)) 
  
p + geom_point()
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

# Customizing your plots

## Shape (scatterplots)

You can customize the shape of the points with 25 different options
![shapes](https://d33wubrfki0l68.cloudfront.net/58a48d625b4bd494cd685dd9998f5c74e9c16907/211c6/visualize_files/figure-html/shapes-1.png)
[Source.](https://r4ds.had.co.nz). Other
[shape](https://ggplot2.tidyverse.org/reference/scale_shape.html)
options.

``` r
p +  geom_point(shape = 23, fill = "violet", color = "black", size = 2.5)
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
p +  geom_point(aes(shape = species, color = species, size = 1.5))
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

## Shape & color manually

You can set manually the color you want to use, with 5 different
[methods](https://www.r-graph-gallery.com/ggplot2-color.html):

  - *Name*: The most common method. R offers about 657 color
    [name](http://www.stat.columbia.edu/~tzheng/files/Rcolor.pdf)
  - *rgb()*: This function allows to build a color using red, green and
    blue values. [RGB
    colors](https://www.rapidtables.com/web/color/RGB_Color.html)
  - *Number*: You can call a color directly by its number
    (`colors()[143]`).
  - *Hex code*: All colors can be defined by their hex code. [Color
    Picker](https://htmlcolorcodes.com/)

<!-- end list -->

``` r
p +  geom_point(aes(shape = species, color = species)) + 
  scale_shape_manual(values = c(15, 16, 17)) +
  scale_color_manual(values = c("darkorange","purple","cyan4")) 
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

## Alpha

Alpha represents the opacity of the geom elements in the plot.

``` r
p +  geom_point(aes(color = species), alpha = 0.6) + 
  scale_color_manual(values = c("darkorange","purple","cyan4")) 
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

## Color palettes

### RColorBrewer

``` r
library(RColorBrewer)

display.brewer.all()
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->
Change manually [Color Brewer Palette](https://colorbrewer2.org)

``` r
p + geom_point(aes(color = species)) +
  scale_color_brewer(palette = "Dark2")
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

### Viridis

viridis colormaps: “magma” (or “A”), “inferno” (“B”), “plasma” (“C”),
“viridis” (“D”), and “cividis” (“E”) viridis direction: 1 colors are
ordered from darkest to lightest, -1 the order is reversed begin & end
options

``` r
library(viridisLite)
library(viridis)

p + geom_point(aes(color = species)) +
  scale_color_viridis(discrete = TRUE, option = "viridis", direction = 1, end = 0.8) 
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

## Changing the legend position

The values for the arguments legend.position are : “left”,“top”,
“right”, “bottom”. They can also be a numeric vector c(x,y) with
values between 0 and 1. c(0,0) corresponds to the “bottom left” and
c(1,1) corresponds to the “top right” position

``` r
pt <- p +  geom_point(aes(color = species)) + 
  scale_color_manual(values = c("darkorange","purple","cyan4")) 

pt + theme(legend.position = "top")
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
# pt + theme(legend.position = c(0, 0.9))
```

## Remove legend, axis titles & axis ticks

``` r
pt + theme(legend.position = "none",
           axis.title = element_blank(),
           axis.ticks = element_blank())
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

## Adding a main title and changing axis titles

``` r
plot <- pt + labs(title = "Penguin size, Palmer Station LTER",
          subtitle = "Flipper length and body mass per Species",
          x = "Flipper length (mm)",
          y = "Body mass (g)",
          color = "Species")

plot
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

### Changing the main title position, font appearance

The most useful arguments of the function element\_text() are: *_color,
size, face, family_* To adjust horizontally (hjust) or vertically
(vjust) you can use the same values between 0 and 1, as we did before,
where 0 corresponds to the “left” and 1 corresponds to the “right”
position

``` r
plot + theme(plot.title = element_text(hjust = 0.5, face = "bold"),
             plot.subtitle = element_text(hjust = 0.5, face = "italic"))
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

## Adding a theme

There are many different themes you can use in ggplot2.
[Here](https://ggplot2.tidyverse.org/reference/ggtheme.html) is a list
of the basic options.

``` r
plot + theme_bw()
```

![](Code-Rladies_june_2020_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

**Other Resources:**

[R for Data
Science](https://r4ds.had.co.nz/data-visualisation.html#fig:shapes) [R
Graphics Cookbook](https://r-graphics.org/)
[ggplot](https://ggplot2.tidyverse.org/index.html) [Data Visualization
with ggplot2](https://viz-ggplot2.rsquaredacademy.com/index.html) [Data
Visualization with R](https://rkabacoff.github.io/datavis/)
[Sthda](http://www.sthda.com/english/wiki/ggplot2-point-shapes)
[Datanovia](https://www.datanovia.com)
[Colors](http://html-color-codes.com/)
