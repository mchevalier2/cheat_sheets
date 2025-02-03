---
title: "Matplotlib/Seaborn cheat sheet"
author: "Manuel"
date: "2025-02-03"
output:
  html_document:
      toc: true
      toc_float: true
---

This document is divided in three sections:

    1. Matplotlib
    2. Seaborn


# 1. Matplotlib



* `import matplotlib.pyplot as plt`
* Standard framework
    * `fig = plt.figure()`
    * Or alternatively for subpltots:
        * `fig, ax = plt.subplots()`
            * This function can be used to split the plotting window (similar to par(mfrow())
                * `plt.subplots(3, 2)` ## 3 lines and 2 columns
            * the `ax` object has now the dimension of the subplot `ax[0, 0].plot()`
            * The option `sharey=True` (“share y axis”) imposes that all the y axes will have the same range
    * `ax.plot()`
    * `plt.show()`
* Parameterize plots
    * `ax.set_xlabel(‘Time (month)’)`
        * the ax object has several methods starting with “set” to parameterise the plot
    * `ax.set_title(“title”)`
    * `ax.set_axis_label(“x-axis-label”, “y-axis-label”)`
    * `ax.tick_params(“y”, colors=‘blue’)` (note the plural of colors here)
    * `ax.set_xticklabels(x, rotation=90)`
    * `ax.errorbar(x, y, yerr=z)`
    * `ax2 = ax.twinx()`
        * Allows adding a second curve with a different y-scale on the same plot.
    * `ax.annotate(text, xy=(posx, posy), xytext=(posx, posy), arrowprops={'arrowstyle': '->', 'color': 'gray'})`
    * markers: `axplot(…, marker=‘o’)`
        * ‘o’ for circles, ‘v’ for inverted triangles ==> https://matplotlib.org/stable/api/markers_api.html
    * linestyle: `axplot(…, linestyle=‘--‘)` to make dashed lines https://matplotlib.org/stable/gallery/lines_bars_and_markers/linestyles.html
    * color: `axplot(…, color=‘r’)`
    * `plt.yscale(‘log’)`
    * `plt.axis('equal')`
        * makes the two axis vary similarly (asp=1 in R)
    * Add a vectical rectangle along axis (like abline but for rectangles)
        * `plt.axvspan(xmin, xmax, alpha=0.5)`



* ADD LINES
    * `plt.axline(xy1 = (xval, yval), slope = 1, linewidth=2, color="green")`
    * `plt.axhline(y=1, linestyle='dotted', linewidth=2, color="green")`



* BARPLOTS
    * `ax.bar(x, y1, label=‘Gold medals’)`
    * `ax.bar(x, y2, bottom=y1, label=‘Silver medals’)`
    * `ax.bar(x, y3, bottom=y1+y2, label=‘Bronze medals’)`
        * Adding labels is necessary for the legend
        * The bar are stacked on top of each other with the bottom parameter
    * ADDING ERROR BARS:
        * `ax.bar(“Gold medals”, y1.mean(), yerr=y1.std())`
            * ?! same function
                * Yes the same. It produces the same figure but with error bars.
    * `ax.legend()`



* HISTOGRAMS:
    * `ax.hist(var_to_plot, label=‘label_for_caption’, bins=10 / [list_of_bin_sizes])`
        * Adding `histtype=‘step’` allows to only plot the outside of the histogram, so that overlapping sections are more visible



* BOXPLOTS;
    * `ax.boxplot([var1, var2])`
    * `ax.set_xticklabels([“lab1”, “lab2”])`


* SCATTERPLOTS
    * `ax.scatter(val1, val2, color=‘blue’, label=‘mnmjn’)`
    * USEFUL TIP: use the c argument to colour code along a third variable. Default seems to be viridis colour scheme
        * `c=val3`


* STYLE
    * `plt.style.use(‘ggplot’)`
        * Call this before the plt.subplots()
        * `plt.style.use(“default’)`
        * https://matplotlib.org/stable/gallery/style_sheets/style_sheets_reference.html


* EXPORT
    * To export figures, use `fig.savefig(“filename.png”, dpi=300)` instead of `plt.show()`
    *  `fig.set_size_inches([5, 3])`




# 2. Seaborn

* Seaborn is built on matplotlib and pandas
    * `import seaborn as sns`
    * `sns.scatterplot(x='life_exp', y='happiness_score', data=world_happiness)`

* You still need to load matplotlib.pyplot as plt. —> `plt.show()`


* RELATIONAL PLOTS
    * `sns.scatterplot(x, y)`
        * `sns.scatterplot(x=‘name_x’, y=‘name_y’, data=df, hue=‘col_to_colour’, palette=colorscale)`
            * `colorscale={‘val1’:’red’, ‘val2’:’black’}`
    * `sns.lineplot()`
        * `ax.wxvline(35)`, `ax.axvline(65)` to add two vertical lines
    * `sns.relplot()` for relation plot. This can make scatter or line plots.
        * The “advantage” is that it can easily create subplots
        * `kind=“scatter” / “line”`
        *` sns.relplot(x, y, data=df, kind=‘scatter’, row/col=var_to_split)`
            * row creates a figure with several rows, col creates a figure with several columns
            * both can be combined using two variables
            * `col_wrap=2` -> will do the same a col but will limit the number of columns to 2 so it wraps on the next line
            * `col_order = [val1, val2, val5, val3, val18]`
            * `size=var_to_size_dots`
            * `hue=var_to_size_dots` is a nice combo with the other one
            * `style`: changes the shape of the dot
            * `alpha`: changes the transparency
            * `markers = True` in case of a lineplot will add a marker on the line
            * `dashes=True/False` for lineplots
            * `palette = sns.color_palette(’Set1’)`
            * for a line plot, if you have several values for x values, it will represent the mean with a CI
                * `ci=“sd”, ci=None`, default (param value unknown at this point) is the 95% interval of the mean



* LINEAR MODELS
    * `sns.regplot(x='life_exp', y='happiness_score', data=world_happiness, ci=None)`
        * A scatter plot with a line, but not a correlation line. it’s a linear model with x as explanatory variable
        * `logistic=True`
    * `sns.lmplot(x='life_exp', y='happiness_score', data=world_happiness, ci=None)`
        * This is a type of FacetGrid plot
    * `sns.residplot(x, y, data=df, lowess=True)`
      `plt.xlabel("Fitted values”)`
      `
plt.ylabel(‘Residuals’)`



* CATEGORICAL PLOTS
    * `sns.countplot(y=var)` y instead of x makes a vertical barplot. Colours are nice
        * `sns.countplot(x’=column_name’, data=df, hue=‘another_col’, hue_order=[val1, val2, val3, ..)`
    * `sns.histplot(x, data, binwidth=0.1)`
        * `sns.histplot(x, y)` makes a 2D map with colours mapping the values in z
    * `sns.catplot()` with advantages similar to relplot()
        * `kind=“count”` plot or `kind=“bar”` plot or `kind=‘box’` for boxplots or `kind=‘point’` for point plots
            * strip, swarm, box, violin, boxen, point, bar, count
        * `order=list_of_ordered_parameters` to sort the type of categories plotted (e.g. if they are ranks for 1 to 5, or days of the week)
        * `sym = ‘’` will remove the outliers on a boxplot
        * `whis=2` (2 times the IQR), `whis=[5, 95]`, `whis=[0,100]` <- min/max values
        * `hue=variable` splits the data in categories (2 boxplots or 2 lines for each x value
        * point plots >> bar plots
        * `join=False` in point plots remove the line connecting the dots
        * `estimator=np.median`
        * `capsize=0.2` changes the length of the top and bottom ticks on error bars
        * `dodge=True` allows for some extra space on the x axis to avoid overlap of data points



* DISTRIBUTION PLOTS
    * `sns.displot(data=taiwan_real_estate, x='price_twd_msq', col='house_age_years', bins=10)`
        * plots histograms in FacetGrid
        * `y` instead of `col` makes a 2D histogram
        * `kind='kde'`



* GENERIC PLOTS
    * `sns.headmap(df.corr(), annot=TRUE); plt.show()`
    * `sns.pairplot(data=df, vars=[var1, var2, var3])`
        * make a scatterplot for each pair of variables selected
    * `sns.kdeplot(data=df, x=var_x, hue="categorical_variable”, cut=0)`
        * Make a kde plot of variable var_x for each level of the categorical variable
        * `cut=0` means that the plot will be cut at 0
        * `cumulative = True` for the cdf
    * `sns.violinplot(x=df['var’])`
    * `sns.boxplot(x, y, data)`
    * `sns.boxenplot(x, y, data)`
        * Revisits the boxplot in, in my opinion, something uglier and less easy to understand
    * `sns.swarmplot()`
        * spreads groups of data with the same x horizontally
    * `sns.jointplot`
        * combines a scatterplot with marginal distributions on top and right sides


* seaborn has 5 figures styles
    * `sns.set_style(style)` white (default), dark, whitegrid, darkgrid, ticks
    * `sns.set(font_scale=1.4)`
    * `sns.set_palette()`
        * embedded palettes (add `“_r”` to palette name to reverse it
            * diverging RdBu PRGn (purple to green),
            * sequential Greys Blues PuRd (light purple to red to dark pink) Purples
            * GnBu (rainfall palette)
        * Add your own with a list of colours
    * `sns.set_context()` paper (default) notebook talk poster


* seaborn returns two object types, usually called g
    * FacetGrid created by relplot and catplot to handle subplots
        * `g.fig.suptitle(“New title”, y=1.03)`
            * y is used to adjust the position of the title which is a bit low by default
        * `g.set_titles(“This is {colname}”)`
            * adds a unique title to each subplot
        * `g.set(xlabel=“lab”, ylabel=“lab”)`
        * `plt.xticks(rotation=90)` to rotation the x labels
            * Note that we go back to matplotlib here!!
        * `plt.subplots_adjust(top=0.9)` brings the title a bit lower
    * AxesSubplot return from single plots
        * `g.set_title(“New title”, y=1.03)`
        * `g.set(xlabel=“lab”, ylabel=“lab”)`
        * `plt.xticks(rotation=90)` to rotation the x labels
            * Note that we go back to matplotlib here!!






##-;
