Personaliza tus gráficos
================
Maggie Suero
6/7/2020

# Personaliza tus gráficos

Vamos a utilizar el
[dataset](https://github.com/allisonhorst/palmerpenguins) de Pingüinos
de Palmer. Estos datos fueron recogidos y están disponibles gracias a la
Dra. Kristen Gorman y la Estación Palmer de la Antártida (Palmer
Station, Antarctica LTER).

Empecemos conociendo a los pingüinos *(Artwork by @allison\_horst)*:

![Palmer
penguins](https://raw.githubusercontent.com/allisonhorst/palmerpenguins/master/man/figures/lter_penguins.png)

## Gráfico básico

``` r
ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point()
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

## Agregando un título principal y modificando los títulos de los ejes

``` r
ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point() +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)")
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

## Forma (para gráficos de dispersión)

Puedes personalizar la forma de los “puntos” de los gráficos de
dispersión utilizando cualquiera de las 25 opciones disponibles

![Formas](https://es.r4ds.hadley.nz/03-visualize_files/figure-html/shapes-1.png)
[Fuente](https://es.r4ds.hadley.nz/visualizaci%C3%B3n-de-datos.html).

``` r
#.... y agrandamos el tamaño de los puntos
ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point(shape = 23, fill = "violet", color = "black", size = 2.5) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)")  
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
# Agregamos la opción de seleccionar la forma de acuerdo a las respuesta de la variable 
ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point(aes(shape = species, color = species)) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)")
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

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
ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point(aes(color = species)) + 
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)",
       color = "Especie")
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

## Alpha

Alpha representa la opacidad o transparencia de los elementos del geom
en el gráfico. Los valores van del 0 (totalmente transparente) al 1
(totalmente visible).

``` r
ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point(aes(color = species), alpha = 0.6) + 
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)",
       color = "Especie")
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

## Paleta de colores

### RColorBrewer

``` r
library(RColorBrewer)

# Nos muestra todas las paletas de colores Brewer
display.brewer.all()
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

Si queremos elegir manualmente alguno de los colores de esta
[paleta](https://colorbrewer2.org) se puede buscar el código del color
deseado o de lo contrario optar por una paleta completa

``` r
ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point(aes(color = species)) +
  scale_color_brewer(palette = "Set2") +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)",
       color = "Especie")
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

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

ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point(aes(color = species)) +
  # Necesitamos indicar que la variable es discreta
  scale_color_viridis(discrete = TRUE, option = "viridis", direction = 1, end = 0.8) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)",
       color = "Especie")
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

Explorando otras
[paletas](https://github.com/EmilHvitfeldt/r-color-palettes)

## Cambiando la posición de la legenda

Los valores válidos para el argumento legend.position son: “left”,“top”,
“right”, “bottom”. También los podemos posicionar utilizando un vector
numérico c(x,y) con valores de 0 a 1. c(0,0) corresponde a la posición
“abajo-izquierda” y c(1,1) a “arriba-derecha”.

``` r
ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point(aes(color = species)) + 
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)",
       color = "Especie") + 
  theme(legend.position = "top")
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

``` r
  # theme(legend.position = c(0.2, 0.7))
```

## Elimando la legenda, los títulos de los ejes y las marcas de los ejes

``` r
ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point(aes(color = species)) + 
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)",
       color = "Especie") + 
  theme(legend.position = "none",
        axis.title = element_blank(),
        axis.ticks = element_blank())
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

### Cambiando la posición del título principal y la apariencia de la fuente

Los argumentos más útiles de la función **element\_text()** son:
*_color, size, face, family_* Para ajustar la posición horizontal
(hjust) o vertical (vjust) podemos utilizar los mismos valores entre 0 y
1 que usamos antes, donde 0 corresponde a la “izquierda” y 1 a la
“derecha”.

``` r
ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point(aes(color = species)) + 
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)",
       color = "Especie") + 
  theme(plot.title = element_text(hjust = 0.5, face = "bold"),
        plot.subtitle = element_text(hjust = 0.5, face = "italic"))
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

## Agregando un tema

Tenemos muchas opciones disponibles para elegir como tema en ggplot2.
[Aquí](https://ggplot2.tidyverse.org/reference/ggtheme.html) hay un
listado de las opciones básicas.

``` r
grafico_pinguinos <- ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point(aes(color = species)) + 
  scale_color_manual(values = c("darkorange","purple","cyan4")) +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal por especie",
       x = "largo aleta (mm)",
       y = "masa corporal (g)",
       color = "Especie") + 
  theme_bw() +
  theme(plot.title = element_text(hjust = 0.5, face = "bold"),
        plot.subtitle = element_text(hjust = 0.5, face = "italic"))

grafico_pinguinos
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

## cómo guardar tu gráfico

``` r
ggsave("~/grafico_pinguinos.png", grafico_pinguinos, width = 7, height = 6)
```

## Extra: cómo resaltar los gráficos

``` r
library(gghighlight)

ggplot(data = pinguinos, aes(x = flipper_length_mm, y = body_mass_g)) + 
  geom_point() + 
  theme_bw() +
  gghighlight(sex == "FEMALE") +
  geom_point(color = "deeppink") +
  labs(title = "Tamaño de los pingüinos, Estación Palmer LTER",
       subtitle = "Largo de la aleta y masa corporal, resaltado en hembras",
       x = "largo aleta (mm)",
       y = "masa corporal (g)") + 
  theme(plot.title = element_text(hjust = 0.5, face = "bold"),
        plot.subtitle = element_text(hjust = 0.5, face = "italic"))
```

![](personaliza_tus_graficos_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

**Otros recursos:**

  - [R para Ciencia de
    Datos](https://es.r4ds.hadley.nz/visualizaci%C3%B3n-de-datos.html)

  - [R Graphics Cookbook](https://r-graphics.org/)

  - [ggplot](https://ggplot2.tidyverse.org/index.html)

  - [Data Visualization with
    ggplot2](https://viz-ggplot2.rsquaredacademy.com/index.html)

  - [Data Visualization with R](https://rkabacoff.github.io/datavis/)

  - [Sthda](http://www.sthda.com/english/wiki/ggplot2-point-shapes)

  - [Datanovia](https://www.datanovia.com)

  - [Colors](http://html-color-codes.com/)

[pingüinos](https://es.greenpeace.org/es/noticias/cual-es-top-de-los-tops-pinguinos-de-la-antartida/)
