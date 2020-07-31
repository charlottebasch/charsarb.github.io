---
layout: post
title:      "Choosing Visualizations"
date:       2020-07-31 23:24:35 +0000
permalink:  choosing_visualizations
---


    When presented with a large dataset, it can be difficult to decide not only on which types of visualizations to use but how to make them. From scatter plots to heat maps and from matplotlib to seaborn to plotly express, there are many options for visualizing your data. In the module one project, I used data about movie budget, gross, genre, year, and IMDB user ratings. Because of the large amount of quantitative data, my mind immediately went to scatter plots. However even with the types of plots chosen, I was left with the choice of using matplotlib, seaborn, and plotly express. In the end I used plots from each of these libraries to tackle the quantitative data. 

Matplotlib:

    The problem with matplotlib plots is that they are not the most visually appealing. They are also quite simple. However when attempting to make a simple scatter plot, sometimes the simplest solution is also the best. I used matplotlib to compare domestic and worldwide box office grosses to movie runtime. I had originally planned to use seaborn to plot both types of gross on the same plot. However there was too much overlap in the data points to see anything clearly, even after changing the opacity of the points. This led me to put the two scatter plots side by side. It can be tempting to try and make a visualization more complicated than it needs to be. Sometimes it feels too ‘easy’ to make a simple scatter plot. However a simple scatter plot can clearly convey a relationship (or lack thereof) between two variables and provide great insight into a question. 

Seaborn:

    While I looked through many types of seaborn plots, it became clear after short search that an lmplot was the best way to examine the relationship between cumulative worldwide gross over a nine year period by movie genre. Because this plot has a regression line and points, it was apparent which movies had an upward trend and which were stabilizing. Using a seaborn lmplot also allowed me to make the plots for all twenty-one genres with only a few lines of code. This plot allowed me to visually compare the slopes. I debated between simply plotting each year’s gross and using cumulative data but ultimately found cumulative data to be more illustrative of a genre’s potential. A disadvantage of this type of plot is the inability to display slope to more rigorously compare the different plots in the lmplot grid. 

Plotly Express:

    While looking at amounts of money brought in by different genres or the production budgets across genre, one factor I wanted to take into account how many movies of each genre were being made. While it may not change cost, it is important for a studio to decide if they’d rather spend their money on multiple cheaper movies or one more expensive movie. I had initially wanted to use seaborn to make a scatter plot of production budget versus worldwide gross color coding each genre and changing the size of each point based on the number of movies it represented. When I executed this plot, I was confused to see that the result was a long axis where each size and each genre were represented. In addition, the colors representing each genre were very close together, which made it difficult to distinguish which point corresponded to each genre. While I was able to split the legend into two sections the same height as the graph using code found on stackoverflow (see 1), this was still not visually appealing and did not solve the confusion over the identity of each point. I attempted to remedy this using code from stackoverflow (see 2). Again this code worked but the points were too close to each other for the labels to be clearly read. 
    This led me to use plotly express. Using this library allows one to build interactive graphs where each point displays its information when hovered over. If a graph needs to contain multiple types of information, using plotly express is a useful solution. In this case, the bubble scatter plots perfectly conveyed the interplay between budget, gross, genre, and number of movies made. Of course plotly express is not only useful when looking at multiple variables. To look at the relationship between average IMDB user ratings and worldwide gross, I used a plotly express scatter plot with a regression line to indicate the lack of relationship between these two variables. In this case I simply preferred the aesthetics of the plotly express version of this plot as opposed to matplotlib or seaborn.    

Other plots:

    Scatter plots are certainly not the be-all and end-all of data visualization. In order to compare the correlations between the quantitative variables I created a seaborn heatmap to display the correlations. The advantages of this type of plot are its clear presentation of statistics and the amount of variables it can compare once without becoming muddy or confusing. Lastly to draw an overall picture of the profitalility of genres, I created a horizontal barplot for each genre that display a genres domestic gross on top of its worldwide gross. Overlaying the domestic gross on the worldwide gross allows a viewer to see not only how much a genre made domestically and internationally, but also see the relative size of domestic gross to worldwide gross. I decided to order the genres by domestic gross in order to clearly see any differences between the top genres internationally and in the United States. It can be harder to see differences in the inner bar than the outer bar so I’ve found ordering the bars this way to help highlight any discrepancies between the total and subtotal. 
    Most of these plots were conceived of by looking through the matplotlib, seaborn, and plotly express examples found on their websites (see 3, 4, 5) and thinking about how my data could be presented using each type of plot. Trial and error was also key. Running into problems helped me gain a deeper understanding of the plots and my data.     

1.	https://stackoverflow.com/questions/56456956/separate-seaborn-legend-into-two-distinct-boxes 
2.	https://stackoverflow.com/questions/46027653/adding-labels-in-x-y-scatter-plot-with-seaborn
3.	https://matplotlib.org/3.1.1/gallery/index.html
4.	https://seaborn.pydata.org/examples/index.html
5.	https://plotly.com/python/plotly-express/

