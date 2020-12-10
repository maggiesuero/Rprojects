Personaliza tus gráficos
================
Maggie Suero
09/12/2020

## Tidyverse

## Introducción al paquete ggplot2

![ggplot2](https://raw.githubusercontent.com/allisonhorst/stats-illustrations/master/rstats-artwork-ES/ggplot2_obra_maestra.png)

*(Artwork by @allison\_horst)*

## Gramática o estructura

\[@CedScherer\](<https://twitter.com/CedScherer/status/1229418108122783744/photo/1>)

1.  Datos (datos que queremos visualizar)
2.  Estéticas (mapeo estético de los objetos)
3.  Capas (formas geométricas y estadísticos)
4.  Escalas (mapeo entre los datos y la dimensión estética)
5.  Sistema de coordenadas (mapeo entre los datos y el plano)
6.  Facetas (grilla de gráficos)
7.  Temas (efectos visuales en general)

Vamos a utilizar el [dataset](https://github.com/cienciadedatos/datos)
traducido al español de la versión
[original](https://github.com/allisonhorst/palmerpenguins) de Pingüinos
de Palmer. Estos datos fueron recogidos y están disponibles gracias a la
Dra. Kristen Gorman y la Estación Palmer de la Antártida (Palmer
Station, Antarctica LTER).

Empecemos conociendo a los pingüinos *(Artwork by @allison\_horst)*:

![Palmer
penguins](https://raw.githubusercontent.com/allisonhorst/palmerpenguins/master/man/figures/lter_penguins.png)

``` r
# Necesitamos instalar el paquete "remotes" para poder acceder a la versión en desarrollo de "datos". Si estuviera en el CRAN se descargaría: install.packages("datos")

#install.packages("remotes")
#remotes::install_github("cienciadedatos/datos")
library(datos)
```

Primera impresión de los datos:

``` r
summary(pinguinos)
```

    ##     especie           isla     largo_pico_mm    alto_pico_mm   largo_aleta_mm 
    ##  Adelia :152   Biscoe   :168   Min.   :32.10   Min.   :13.10   Min.   :172.0  
    ##  Barbijo: 68   Dream    :124   1st Qu.:39.23   1st Qu.:15.60   1st Qu.:190.0  
    ##  Papúa  :124   Torgersen: 52   Median :44.45   Median :17.30   Median :197.0  
    ##                                Mean   :43.92   Mean   :17.15   Mean   :200.9  
    ##                                3rd Qu.:48.50   3rd Qu.:18.70   3rd Qu.:213.0  
    ##                                Max.   :59.60   Max.   :21.50   Max.   :231.0  
    ##                                NA's   :2       NA's   :2       NA's   :2      
    ##  masa_corporal_g     sexo          anio     
    ##  Min.   :2700    hembra:165   Min.   :2007  
    ##  1st Qu.:3550    macho :168   1st Qu.:2007  
    ##  Median :4050    NA's  : 11   Median :2008  
    ##  Mean   :4202                 Mean   :2008  
    ##  3rd Qu.:4750                 3rd Qu.:2009  
    ##  Max.   :6300                 Max.   :2009  
    ##  NA's   :2

``` r
#Omitimos los valores perdidos
pinguinos <- na.omit(pinguinos)
```

#### Gráfico básico

``` r
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) + 
  geom_point()
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

## Forma (para gráficos de dispersión)

Podemos personalizar la forma de los “puntos” de los gráficos de
dispersión utilizando cualquiera de las 25 opciones disponibles

![Formas](https://es.r4ds.hadley.nz/03-visualize_files/figure-html/shapes-1.png)
[Fuente](https://es.r4ds.hadley.nz/visualizaci%C3%B3n-de-datos.html).

``` r
#.... y agrandamos el tamaño de los puntos
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(shape = 23, fill = "violet", color = "black", size = 2.5) 
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
# Agregamos la opción de seleccionar el color de acuerdo a las respuesta de la variable 
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(color = especie)) 
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
# Combinamos el color y la forma 
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(shape = especie, color = especie)) 
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

## Establecer el color manualmente

Podemos establecer manualmente el color que queramos utilizar en los
gráficos, de 5
[maneras](https://www.r-graph-gallery.com/ggplot2-color.html)
diferentes:

  - *Por nombre*: es el método más común. R ofrece 657 colores para
    elegir
    [nombre](http://www.stat.columbia.edu/~tzheng/files/Rcolor.pdf)
  - *rgb()*: esta función permite elegir colores utilizando los valores
    de rojos (“R” - red), verdes (“G” - green) y azules (“B” - blue).
    [RGB colors](https://www.rapidtables.com/web/color/RGB_Color.html)
  - *Numérica*: se puede llamar directamente al color por su número, por
    ejemplo `colors()[143]`.
  - *Código hexadecimal*: se puede utilizar los valores de los códigos
    hex. [Color Picker](https://htmlcolorcodes.com/)

<!-- end list -->

``` r
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(shape = especie, color = especie)) +
  scale_color_manual(values = c("darkorange","purple","cyan4")) 
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(color = especie)) +
  scale_color_manual(values = c("darkorange","purple","cyan4")) 
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

## Alpha

Alpha representa la opacidad o transparencia de los elementos del geom
en el gráfico. Los valores van del 0 (totalmente transparente) al 1
(totalmente visible).

``` r
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(color = especie), alpha = 0.6) +
  scale_color_manual(values = c("darkorange","purple","cyan4"))
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

## Paleta de colores

### RColorBrewer

``` r
library(RColorBrewer)

# Nos muestra todas las paletas de colores Brewer
display.brewer.all()
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

Si queremos elegir manualmente alguno de los colores de esta
[paleta](https://colorbrewer2.org) se puede buscar el código del color
deseado o de lo contrario optar por una paleta completa

``` r
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(color = especie)) +
  scale_color_brewer(palette = "Set2") 
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

### Viridis

Las opciones de colores de la paleta de Viridis son: “magma” (“A”),
“inferno” (“B”), “plasma” (“C”), “viridis” (“D”), and “cividis” (“E”).
Podemos elegir la dirección de los colores con “direction”. Por defecto,
“direction = 1”, por lo que los colores están ordenados de oscuros a
claros. Si la cambiamos a “direction = -1”, los invertimos. La paleta
también permite elegir en qué color queremos comenzar y terminar,
modificando los parámetros “begin” y “end” con valores de 0 a 1.

``` r
library(viridisLite)
library(viridis)

ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(color = especie)) +
  # Necesitamos indicar que la variable es discreta
  scale_color_viridis(discrete = TRUE, option = "viridis", direction = 1, end = 0.8) 
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

Explorando otras
[paletas](https://github.com/EmilHvitfeldt/r-color-palettes)

## Cambiando la posición de la legenda

Los valores válidos para el argumento legend.position son: “left”,“top”,
“right”, “bottom”. También los podemos posicionar utilizando un vector
numérico c(x,y) con valores de 0 a 1. c(0,0) corresponde a la posición
“abajo-izquierda” y c(1,1) a “arriba-derecha”.

``` r
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(color = especie)) +
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  theme(legend.position = "top")
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

``` r
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(color = especie)) +
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  theme(legend.position = c(0.2, 0.7))
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

## Elimando la legenda, los títulos de los ejes y las marcas de los ejes

``` r
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(color = especie)) +
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  theme(legend.position = "none",
        axis.title = element_blank(),
        axis.ticks = element_blank())
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

## Agregando un título principal y modificando los títulos de los ejes

``` r
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(color = especie)) +
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)")
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

### Cambiando la posición del título principal y la apariencia de la fuente

Los argumentos más útiles de la función **element\_text()** son:
*_color, size, face, family_* Para ajustar la posición horizontal
(hjust) o vertical (vjust) podemos utilizar los mismos valores entre 0 y
1 que usamos antes, donde 0 corresponde a la “izquierda” y 1 a la
“derecha”.

``` r
ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(color = especie)) +
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)") +
  theme(plot.title = element_text(hjust = 0.5, face = "bold"),
        plot.subtitle = element_text(hjust = 0.5, face = "italic"))
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

## Agregando un tema

Tenemos muchas opciones disponibles para elegir como tema en ggplot2.
[Aquí](https://ggplot2.tidyverse.org/reference/ggtheme.html) hay un
listado de las opciones básicas.

``` r
grafico_pinguinos <- ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point(aes(color = especie)) +
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)",
       caption = "@G33kyCats") +
  theme_bw() +
  theme(plot.title = element_text(hjust = 0.5, face = "bold"),
        plot.subtitle = element_text(hjust = 0.5, face = "italic"),
        plot.caption = element_text(face = "italic", size = 10))

grafico_pinguinos
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

## cómo guardar tu gráfico

``` r
ggsave("C:/Users/Maggie/OneDrive/aR/Rprojects/grafico_pinguinos.png", grafico_pinguinos, width = 7, height = 6)
```

## Extra: cómo resaltar los gráficos

``` r
library(gghighlight)

ggplot(data = pinguinos, aes(x = largo_aleta_mm, y = masa_corporal_g)) +
  geom_point() +
  theme_bw() +
  gghighlight(sexo == "hembra") +
  geom_point(color = "deeppink") +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal, resaltado en hembras",
       x = "largo aleta (mm)",
       y = "masa corporal (g)") +
  theme(plot.title = element_text(hjust = 0.5, face = "bold"),
        plot.subtitle = element_text(hjust = 0.5, face = "italic"))
```

![](RladiesMVD_personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

**Otros recursos:**

  - [R para Ciencia de
    Datos](https://es.r4ds.hadley.nz/visualizaci%C3%B3n-de-datos.html)

  - [Hoja de Referencia -
    RStudio](https://rstudio.com/wp-content/uploads/2015/04/ggplot2-spanish.pdf)

  - [R para profesionales de los datos: una
    introducción](https://www.datanalytics.com/libro_r/elementos-de-un-grafico-en-ggplot2.html)

  - [R Graphics Cookbook](https://r-graphics.org/)

  - [Data Visualization with
    ggplot2](https://viz-ggplot2.rsquaredacademy.com/index.html)

  - [Data Visualization with R](https://rkabacoff.github.io/datavis/)

  - [Sthda](http://www.sthda.com/english/wiki/ggplot2-point-shapes)

# Bonus Track: Recursos y Comunidades R

  - [Comunidad R para Ciencia de Datos](https://twitter.com/r4ds_es)

  - [\#30díasdegráficos con
    R](https://github.com/cienciadedatos/datos-de-miercoles/blob/master/30-dias-de-graficos-2020.md)

  - [R-Ladies Global](https://rladies.org/)

  - [R-Ladies Global meetup](https://www.meetup.com/es-ES/pro/rladies)

  - [RLadies en Argentina
    durante 2020](https://rladiesenargentina.github.io/Resumen_meetups_2020/)

  - [Lista
    RLadies](https://twitter.com/i/lists/1299748905463222273?s=20)
