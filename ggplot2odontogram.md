ggplot2\_odontogram
================

## Codification

This is a graphic template to generates odontogram from oral exam data.
The data format is based on dental chart ISO 3950 notation, with 6
surface descriptors on each teeth.

## How to use it

Dataframe to graph odontogram has 5 column:  
\-x,y: coordinates of each point  
\-t:grouping codification: \[teeth number\]\[surface\]  
\-pos: surface code: d:distal m:mesial o:oclusal b:bucal l:lingual  
\-lab: a label column 1 for each teeth number

``` r
hd(odgr)
```

    ##   x y   t pos  lab
    ## 1 1 4 18m   m <NA>
    ## 2 2 5 18m   m <NA>
    ## 3 2 6 18m   m <NA>
    ## 4 1 7 18m   m <NA>
    ## 5 1 4 18l   l   18
    ## 6 4 4 18l   l <NA>

## Plot result

Using ggplot2 you can obtain:

``` r
ggplot() +
  geom_polygon(data=odgr, mapping=aes(x=x, y=y,group=t,fill=pos))+
  geom_hline(yintercept = 0)+
  geom_vline(xintercept = 28.7)+
  geom_text(data=odgr[!is.na(odgr$lab),], 
            aes(x=x, y=y, label=lab), hjust=0, vjust=1, size=3)+
  theme_void()+
  scale_fill_brewer(palette="Paired",name="Surface:",
                    labels=c("Distal","Facial","Lingual","Mesial","Oclusal"))
```

![](ggplot2odontogram_files/figure-gfm/pressure-1.png)<!-- -->
