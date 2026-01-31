

# Matplotlib (Python) 

    This folder contains hands-on learning notes and practice scripts for **Matplotlib**, the core Python library for creating visualizations. I used Matplotlib to plot lines, bars, histograms, scatter plots, filled area charts, time series, and real-time updating charts. Most examples use pandas DataFrames and NumPy arrays.

# Basic Plot Structure
    - Importing Matplotlib and plotting data
    - Adding titles and axis labels
    - Showing and saving figures

# Line Plots

    Used for trends and continuous data. plt.plot(x, y)

# Bar Charts

    Used for comparing categories or counts
    plt.bar(x_index, y)
    plt.barh(languag, popularity)    # barh interchange the axis

# PIE Charts

# Stackplots

    Used to show how multiple categories contribute to a total over time.
    plt.stackplot(x, a, b, c, labels=["A", "B", "C"])


# Histograms

    Used to understand how values are spread 
    plt.hist(ages, bins=20)

# Scatter Plots

    Used to see relationships between two numeric variables.
    plt.scatter(x, y, alpha=0.5)

# Time Series Plots
    
    Used for plotting data over time.
    plt.plot(weekly.index, weekly["MathScore"])

# Saving Figures

    Export plots for reports and dashboards.
    plt.savefig("plot.png", dpi=200, bbox_inches="tight")

# Plotting Live Data (Real-Time)

    matplotlib.animation.FuncAnimation

[Corey Schafer](https://www.youtube.com/watch?v=YYXdXT2l-Gg&list=PL-osiE80TeTt2d9bfVyTiXJA-UTHn6WwU)