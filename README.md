# Global-Scientific-Production-Template

## Includes Log Coloring, 1:110m Scale, and Labels

**Updated:** June 21, 2025

---
## Table of Contents
- [Description](#description)
- [Technology Used](#technology-used)
- [How to Update the Map with New Data](#how-to-update-the-map-with-new-data)
  - [Step 1. Process data in R](#step-1-process-data-in-r)
  - [Step 2. Update the Observable Excel file](#step-2-update-the-observable-excel-file)
  - [Step 3. Replace the file in Observable](#step-3-replace-the-file-in-observable)
- [Custom Visualization Tweaks](#custom-visualization-tweaks)
  - [Display Only the Top n Countries](#display-only-the-top-n-countries)
  - [Extract Top Countries from Data](#extract-top-countries-from-data)
  - [Special Case Capitalization for Country Names](#special-case-capitalization-for-country-names)
  - [Custom Styling for Text Labels](#custom-styling-for-text-labels)
  - [Custom Legend Title and Position](#custom-legend-title-and-position)
  - [Labeling Only the Top n Countries on the Map](#labeling-only-the-top-n-countries-on-the-map)
- [Color Options for the Map](#color-options-for-the-map)
  - [Usage](#usage)
  - [Available Color Interpolators](#available-color-interpolators)
- [How to Download the Map (SVG or PNG)](#how-to-download-the-map-svg-or-png)
  - [Option 1: From the chart menu (top-right corner)](#option-1-from-the-chart-menu-top-right-corner)
  - [Option 2: From the button below the map](#option-2-from-the-button-below-the-map)
- [Contributors](#contributors)
- [Citation](#citation)
  - [APA style](#apa-style)
  - [BibTeX](#bibtex)
---

### Description <p style="font-size: 0.8em;">🔝 <a href="#table-of-contents">Toc</a></p>

This interactive map is inspired by the original work *CountrySciProd Project* by [AlexanderRV22](https://github.com/Alex-rv150/CountrySciProud), which offers a global overview of **scientific production** through visual analytics. Building on that foundation, this version incorporates enhancements such as:

- Logarithmic color scale.
- 1:110m small scale projection.
- Dynamic country labels displaying names and frequencies.

Designed for researchers, educators, and policymakers, this tool allows users to explore how different countries contribute to scientific research. The visualization supports deeper insights into scientific output worldwide, and the code can be easily modified to reflect custom frequency data or labeling preferences.

View the full [here](https://observablehq.com/d/ec528de5c6f1cd3d). 

![image](https://github.com/user-attachments/assets/3b57f30e-38ea-42f6-9c59-c570dbf1413f)

---

### Technology Used

This interactive map was built using `JavaScript` with the `D3.js` library. The implementation includes:

- Logarithmic and sequential color scales (`d3.scaleSequentialLog`, `d3.interpolateRgb`)

- Geospatial rendering with `d3.geoPath` and `TopoJSON`

- Interactive labeling and zoom features

- Customizable color interpolators for user-defined styles

  > All code is written in `JavaScript` and can be directly edited within an `Observable notebook`, or adapted for any HTML-based environment.
---

### How to Update the Map with New Data

If you want to update the map with a new frequency dataset (e.g., number of publications, citations, or any other metric), follow these steps:


##### Step 1. Process data in R

Use the provided `R` script to:

- Load the Excel file exported from `biblioshiny` library (e.g., `BiblioshinyReport1.xlsx`).

- Convert country names to `ISO2` codes.

- Export the updated file in the required format.

  > The full script is [available here](https://github.com/hllinas/Global-Scientific-Production-Template/blob/main/Observable.Rmd) and is also included in this repository.


##### Step 2. Update the Observable Excel file

- Download the `Data_obs.xls` file currently used in your `Observable notebook` by clicking the file icon 📎 in the right-hand panel (top-right corner of the notebook interface), under  `File attachments`. Then, locate the `Data_obs.xlsx` file, click the three vertical dots (`⋮`) next to it, and select `Download`.

- Open the sheet named `Sheet6`.

- Copy and paste the columns `CountryCode` and `Freq` from the R-exported file into columns 1 and 2 of `Sheet6`.
  
  > Do not modify: 
  > - The red-coded third column in `Sheet6`.
  > - Any sheet name.

##### Step 3. Replace the file in Observable
   
- Upload your updated `Data_obs.xlsx` back to the `Observable notebook`. Go to the File attachments panel (📎 icon, top-right corner), locate the existing `Data_obs.xlsx`, click the three dots (`⋮`), and select `Replace file`. Then, upload your newly updated file.
  
- Run the notebook to regenerate the map with updated data.

  > This method ensures your visualization stays up to date with the latest scientific production metrics, while keeping the internal map logic unchanged.

### Custom Visualization Tweaks

This project includes some small but helpful code adaptations to improve the visualization experience. These changes are completely optional — feel free to modify or extend them based on your preferences or the needs of your dataset.


####  Display Only the Top n Countries

If you'd like to limit the number of countries displayed (e.g., top n=5), you can define it like this:

```js
// Display only the top n countries
const n = 5;
```


#### Extract Top Countries from Data

You can use the following function to sort your dataset by frequency, take the top n countries, and enrich the result with country names:

```js
function getTopCountries(data, countryCodes, n) {
  // Sort by frequency (descending)
  const sorted = [...data].sort((a, b) => b.B - a.B);
  
  // Get top N
  const top = sorted.slice(0, n);

  // Enrich with country names if available
  const topWithNames = top.map(entry => {
    const match = countryCodes.find(c => c["country-code"] == entry.C);
    return {
      code: entry.C,
      name: match ? match.name.toUpperCase() : "Unknown",
      freq: entry.B
    };
  });

  return topWithNames;
}
```

#### Special Case Capitalization for Country Names

To ensure that some country names like UK, USA, and Emirates are shown in their usual abbreviated form while other names are capitalized normally:

```js
const uk = "UK";
const usa = "USA";
const uae = "Emirates";

function capitalizeWords(text) {
  const lowerText = text.toLowerCase();

  if (lowerText === uk.toLowerCase() || lowerText === usa.toLowerCase()) {
    return text; // Keep abbreviation as-is
  } else {
    return text
      .toLowerCase()
      .split(' ')
      .map(word => word.charAt(0).toUpperCase() + word.slice(1))
      .join(' ');
  }
}
```

#### Custom Styling for Text Labels

Here’s an example of how to customize label appearance — including font, fill color, stroke, and position:

```js
.attr("text-anchor", "middle")      // Text alignment
.attr("font-size", "15px")          // Font size
.attr("fill", "black")              // Fill color
.attr("stroke", "white")            // Stroke (outline) color
.attr("stroke-width", 2)            // Stroke width
.attr("paint-order", "stroke")      // Draw stroke behind fill
.attr("x", 50)                      // X position of the label
.attr("y", 430)                     // Y position of the label
.attr("font-family", "arial")       // Font family
.attr("font-size", "15px")          // Text size
.attr("fill", "black")              // Text color
.attr("text", "1:110m small scale") // Text content
```

#### Custom Legend Title and Position

If you want to reposition the legend or change its title and tick formatting, you can adapt the following snippet. This example places the legend at coordinates `(650, 380)` and sets the title to `"Log of CountrySciProd"` with 6 ticks and a custom format:

```js
svg.append("g")
  .attr("transform", "translate(650, 380)") // Change position of the legend
  .append(() => {
    return Legend(scale, {
      title: "Log of CountrySciProd", // Title displayed above the legend
      ticks: 6,                       // Number of tick marks to display on the scale
                                      // e.g., 6 tick values like 1, 10, 100, 1k, 10k, 100k
                                      // (for log scale)
      tickFormat: ".0f"               // Format for tick labels
                                      // (e.g., ".2s" for 1k, ".0f" for integers)
    });
  });
```

#### Labeling Only the Top n Countries on the Map

To annotate only the top `n` countries based on frequency, you can use the result of `getTopCountries(...)` to filter which countries will display labels. This ensures that your map remains clean and focused:

```js
const top = getTopCountries(data, countryCodes, n); // Get top n countries

g.selectAll("text.label")
  .data(topojson.feature(world, world.objects.countries).features) // Convert TopoJSON to GeoJSON
  .enter()
  .filter(d => top.some(p => p.code == d.id)) // Show labels only for top countries
  .append("text")
  .attr("class", "label")
  .attr("transform", d => {
    const centroid = path.centroid(d); // Calculate the label's position
                                       // (center of the country shape)
    return `translate(${centroid[0]},${centroid[1]})`;
  });
```

  > These customizations are just suggestions. You are free to adapt, extend, or redesign them to better suit your project’s style and needs.
---

### Color Options for the Map

This section provides a collection of color scale combinations that you can apply to the Global Scientific Production Template. These color interpolators can be used to highlight scientific production frequencies in different styles, helping tailor the visual experience to your goals.

#### Usage

You can apply any interpolator like this:

```js
const scale = d3.scaleSequentialLog(colorInterpolators.cyanToBlue)
                .domain([0.9, 2500]);
```

Or use a linear scale instead:

```js
const scale = d3.scaleSequential(colorInterpolators.skyblueToMidnightBlue)
                .domain([0, 200]);
```

#### Available Color Interpolators

Below is a comprehensive set of custom interpolators that you can copy and use directly in your project:

```js
const colorInterpolators = {
  cyanToBlue: d3.interpolateRgb("cyan", "blue"),
  aquamarineToGreen: d3.interpolateRgb("aquamarine", "green"),
  mistyroseToOrange: d3.interpolateRgb("mistyrose", "orange"),
  mistyroseToGreen: d3.interpolateRgb("mistyrose", "green"),
  azureToDarkOrchid: d3.interpolateRgb("azure", "darkorchid"),
  lightGreyToViolet: d3.interpolateRgb("lightgrey", "violet"),
  lightCyanToTeal: d3.interpolateRgb("lightcyan", "teal"),
  blueToNavy: d3.interpolateRgb("lightblue", "navy"),
  greenToDarkGreen: d3.interpolateRgb("lightgreen", "darkgreen"),
  yellowToRed: d3.interpolateRgb("yellow", "red"),
  whiteToPurple: d3.interpolateRgb("white", "purple"),
  lightGreyToDarkBlue: d3.interpolateRgb("lightgrey", "darkblue"),
  orangeToBrown: d3.interpolateRgb("orange", "brown"),
  skyblueToMidnightBlue: d3.interpolateRgb("skyblue", "midnightblue"),
  pinkToFuchsia: d3.interpolateRgb("pink", "fuchsia"),
  lightYellowToDarkGreen: d3.interpolateRgb("lightyellow", "darkgreen"),
  beigeToSaddleBrown: d3.interpolateRgb("beige", "saddlebrown"),
  lavenderToIndigo: d3.interpolateRgb("lavender", "indigo"),
  whiteToLightBlue: d3.interpolateRgb("white", "lightblue"),
  yellowToBlue: d3.interpolateRgb("yellow", "blue"),
  lightGreenToDarkBlue: d3.interpolateRgb("lightgreen", "darkblue"),
  lightPinkToDarkRed: d3.interpolateRgb("lightpink", "darkred"),
  lightGreyToDarkGreen: d3.interpolateRgb("lightgrey", "darkgreen"),
  lightSalmonToDarkRed: d3.interpolateRgb("lightsalmon", "darkred"),
  lightYellowToDarkGoldenrod: d3.interpolateRgb("lightyellow", "darkgoldenrod"),
  lightGreenToDarkTurquoise: d3.interpolateRgb("lightgreen", "darkturquoise")
};
```
Feel free to experiment with these combinations and adjust the domain based on your data range.

  > These color scales were designed to offer flexibility for thematic visualizations and can be adapted for different map layers, legends, or user-driven filters.
---

### How to Download the Map (SVG or PNG)

You can easily export the map visualization for use in reports, presentations, or publications.

#### Option 1: From the chart menu (top-right corner)

1. Hover over the map until the **three-dot menu** (`⋮`) appears in the top-right corner.
2. Click on it to open the options.
3. Choose:
   - `Download SVG`:  to export a high-quality scalable vector graphic.
   - `Download PNG`: to export a standard image file.


#### Option 2: From the button below the map

If available, a `Save as SVG` button is shown directly beneath the map. Click it to instantly download the SVG file.

> Tip: SVG files are ideal for high-resolution printing or editing in tools like Adobe Illustrator, Inkscape, or PowerPoint.
---

### Contributors

- Dr. rer. nat. Humberto Llinás Solano (hllinas@uninorte.edu.co)¹ 
- Alexander Rangel Vizcaíno (alexanderrangel@uninorte.edu.co)¹
- Daniela Nuñez Guzmán (nunezdm@uninorte.edu.co)¹
- Humberto LLinás Marimón (lhumberto@uninorte.edu.co)²

  > ¹ Department of Mathematics and Statistics, Universidad del Norte, Barranquilla, Colombia.
  > 
  > ²  Department of Systems Engineering, Universidad del Norte, Barranquilla, Colombia.
---

### Citation

To cite this repository in your academic work, teaching, or research:

#### APA style

> Llinás Solano, H., Rangel Vizcaíno, A., Nuñez Guzmán, D. & LLinás Marimón, H. (2025). *Global-Scientific-Production-Template* [GitHub repository].
                    GitHub.[https://github.com/hllinas/Global-Scientific-Production-Template/tree/main](https://github.com/hllinas/Global-Scientific-Production-Template/tree/main)
#### BibTeX

```bibtex
@misc{llinas2025timeline,
  author       = {Humberto Llinás Solano, Alexánder Rangel Vizcaíno,
                  Daniela Nuñez, Humberto Llinás Marimón},
  title        = {Global-Scientific-Production-Template},
  year         = {2025},
  howpublished = {\url{https://github.com/usuario/statistical-timeline}},
  note         = {GitHub repository}
}
```
