---
layout: tutorial
label: PlotCoverage
title: Plot per base coverage of genomic features
---




## Plotting the per base coverage of genomic features

The **kpPlotCoverage** function is similar to 
[kpPlotDensity]({{ site.baseurl }}{% link Tutorial/PlotDensity/PlotDensity.md %})
but instead of plotting the number of features overalpping a certain genomic window,
it plots the actual number of features overlapping every single base of the genome.
Conceptually, it is equivalent to `kpPlotDensity` with _window.size_ set to 1 but
much faster, since internally it uses the `coverage` method from 
[GenomicRanges](https://bioconductor.org/packages/GenomicRanges).



```r
library(karyoploteR)
regions <- createRandomRegions(nregions=10000, length.mean = 1e6, mask=NA)
kp <- plotKaryotype()
kpPlotCoverage(kp, data=regions)
```

![plot of chunk Figure1](images//Figure1-1.png)

The actual representation of the data is also different than that of 
`kpPlotDensity`: **kpPlotCoverage** uses **kpBars** to create the plot, giving 
it a histogram-like appearance.

We can plot the actual regions in data panel 2 to see how they relate


```r
kp <- plotKaryotype(plot.type=2, chromosomes = "chr21")
kpPlotCoverage(kp, data=regions)
kpPlotRegions(kp, data=regions, data.panel=2)
```

![plot of chunk Figure2](images//Figure2-1.png)

It is possible to customize the appearance of the coverage plot using the same 
parameters used for 
[kpRect]({{ site.baseurl }}{% link Tutorial/Rectangles/Rectangles.md %}).



```r
more.regions <- createRandomRegions(nregions=40000, length.mean = 1e6, mask=NA)
kp <- plotKaryotype(plot.type=1, chromosomes = "chr21")
kpPlotCoverage(kp, data=more.regions, r0=0.7, r1=1, col="#0e87eb")
kpPlotCoverage(kp, data=more.regions, r0=0.7, r1=0.85, col="#ffdb50")
kpPlotRegions(kp, data=more.regions, r0=0.65, r1=0)
```

![plot of chunk Figure4](images//Figure4-1.png)
