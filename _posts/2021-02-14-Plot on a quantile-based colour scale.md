---
title: "Plot a raster map on a quantile-based colour scale"
layout: post
category: coding
---




Sometimes you need to display images with a very skewed values distribution, like the image below, which you can barely see because most cell values are very low, but very few are very high. You can see how right-skewed the distribution of the map values is by plotting their histogram. The histogram on the left is of the whole set of values in the raster, while the histogram on the right shows only the cells with values smaller than 2. Because only few cells have very high values - the maximum of value in the raster is 7.77 - they appear too small to be seen, and the map looks flat.

![plot of chunk plot](/figures/plot-1.svg)


If you have a raster like this, you may want to address the issue by looking at what caused the skewness in the first place. However, if you just want to see what is there in the data, the solution may be to bin its values into sets that contain the same number of observations (i.e. quantiles), and attribute all values in each bin the same colour.

To do this you can use the following function:


    # Function to plot a raster by using colour break points at quantiles.
    
    qplot<-function(r, Nclass, palette = c('grey95','grey5'),
                    main = "auto", ...){
      
      # r:          Raster
      # Nclass:     Integer. Number of colour classes. r values will be divided in
      #             Nclass bins, each containing the same number of values.
      # palette:    Character string defining the extremes of the colour palette.
      # ...:        Additional parameters passed to function plot().
      
      vls <- na.omit(extract(r,extent(r)))
      ntrvls <- classInt::classIntervals(vls,n=Nclass)$brks
      pal <- colorRampPalette(palette)
      clrint <- pal(Nclass+1)
      ll <- seq(min(ntrvls), max(ntrvls), length.out = 4)
      if (main == "auto"){
        main = paste0(names(r), "\n(Quantile color progression)")
      }
      plot(r, breaks=ntrvls, col=clrint,
           axis.args = list(at = ll, labels = as.character(round(ll,2))),
           main = main)
      
    }

The function requires package `classInt` and uses it to define a user-defined number quantile bins. Then it uses `colorRampPalette` to interpolate the colours you want your image to be plotted with and attributes equally spaced gradations of the obtained palette to each quantile. The funciton also adds a default subtitle to remind you that the displayed image is not plotted on a linear scale.

For example, using the function on the above right skewed map looks like this:


    # "map" is an example right-skewed RasterLayer
    # Create colour palette with RColorBrewer
    library(RColorBrewer)
    myPal <- brewer.pal(n = 9, name = "YlOrRd")
    
    # Quantile-plot the right-skewed raster
    qplot(map, 50, myPal)

![plot of chunk example](/figures/example-1.svg)

The spatial distribution of values is now visible. The advantage of this method is that it will work no matter what kind of skewness your data has!
