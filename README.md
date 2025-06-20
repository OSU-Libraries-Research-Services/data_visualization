# What is Data Visualization


# What is data visualization?

Stephen Few defines data visualization as "all types of visual representations that support the exploration, examination, and communication of data" in his book __[Now You See It: Simple Visualization Techniques for Quantitative Analysis](https://olc1.ohiolink.edu/record=b27686243)__. Visualized data can help us efficiently and effectively summarize data. It can also help you observe patterns you might miss if you examined the raw data alone (e.g., __[Anscombe’s Quartet](https://en.wikipedia.org/wiki/Anscombe%27s_quartet)__). 

<!-- <div class="video-container">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/YDT5ZPcMZWM" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div> -->

:::{iframe} https://www.youtube.com/embed/YDT5ZPcMZWM
:width: 100%

:::

# Why visualize data?

Visualized data can help us ...
- **spot trends**
- **identify patterns**, and
- **quickly make sense** of our data. 

It can also help us share our data in meaninful and effective ways.

+++

# How should I visualize data?

## 👥 Know your audience
Before you create a chart, consider your purpose. Are you explaining a concept or exploring a pattern? Will your audience benefit more from a simple, clear visual or a more complex, detailed one? Tailoring your visualization to your audience’s needs is key to making your data meaningful.
## Apply visual best practices
### 📊 Choose the right chart for your data
Selecting the best chart type is one of the most important—and sometimes most challenging—parts of data visualization. Fortunately, a small set of well-designed charts can meet most needs when used thoughtfully.

- The **__[Financial Times Visual Vocabulary](https://ft-interactive.github.io/visual-vocabulary/)__** provides a **visual taxonomy** — or categorized collection of chart types — organized by the kind of relationship or message you want to show — such as change over time, distribution, ranking, or correlation. It helps answer the question: ***“What’s the best way to visualize this data?”***

![Financial Times Visual Vocabulary](images/ft_thumbnail.png)

- **__[Abela's Chart Chooser](https://extremepresentation.typepad.com/files/choosing-a-good-chart-09.pdf)__** helps you select a chart based on the number of measures and dimensions in your data.

- Stephanie Evergreen's **Quantitative Chart Chooser** published on the inside front cover of her book __[Effective Data Visualization: the Right Chart for the Right Data](https://library.ohio-state.edu/record=b10327021~S7)__, guide you based on your **communication goal.** Are emphasizing a single number? Showing change over time? Comparing to a benchmark? This tool guides you through those decisions.

Evergreen also provides a **Qualitative Chart Chooser** on the inside back cover and dedicates an entire chapter to helping you determine the best ways to present qualitative data effectively.

### 🎨 Use colors and fonts wisely 
- Limit your color palette to maintain clarity and accessbility.
- Use color to emphasize key point.
- Stciek to clean, readable fonts and avoid unnecessary styling.

### ✂️ Less is better.
- Simplify your chart.
- Remove tick marks and grid lines that do not add value.
- Label data point directly when possible to reduce cognitive load.
- Aim for clarity over complexity — less is often more!

## 🖱️ Add interactivity (when appropriate)
Interactive tools like **Tableau**, **RShiny**, or **Power BI** allow users to explore data on their own.
- Use filters to let users drill down from high-level overviews to detailed views.
- Structure interactivity to support meaningful exploration.


## 🧭 Provide context and clear instructions
- Don't assume your audience knows how to interpret your chart.
- Include a clear title that communicates the key takeaway.
- Add brief instructions or a help link if your visualization is interactive.
- Provide context for your data source(s).
- Always cite your data source(s).


## 🧪 Test your visualization
Before sharing, ask a colleague or friend to critique your chart:
- Do they understand the message?
- Can they use the filters (if interactive)?
- Does the visual guide them to the insight you intended?
