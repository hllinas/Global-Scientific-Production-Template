# Global-Scientific-Production-Template

## Includes Log Coloring, 1:110m Scale, and Labels

**Updated:** June 21, 2025

This interactive map is inspired by the original work *CountrySciProd Project* by [AlexanderRV22](https://github.com/Alex-rv150/CountrySciProud), which offers a global overview of **scientific production** through visual analytics. Building on that foundation, this version incorporates enhancements such as:

- Logarithmic color scale.
- 1:110m small scale projection.
- Dynamic country labels displaying names and frequencies.

Designed for researchers, educators, and policymakers, this tool allows users to explore how different countries contribute to scientific research. The visualization supports deeper insights into scientific output worldwide, and the code can be easily modified to reflect custom frequency data or labeling preferences.

View the full [here](https://observablehq.com/d/ec528de5c6f1cd3d). 

![image](https://github.com/user-attachments/assets/3b57f30e-38ea-42f6-9c59-c570dbf1413f)

---

### Technology Used

This interactive map was built using JavaScript with the `D3.js` library. The implementation includes:

- Logarithmic and sequential color scales (`d3.scaleSequentialLog`, `d3.interpolateRgb`)

- Geospatial rendering with `d3.geoPath` and `TopoJSON`

- Interactive labeling and zoom features

- Customizable color interpolators for user-defined styles

  > All code is written in JavaScript and can be directly edited within an Observable notebook, or adapted for any HTML-based environment.

---

### How to Update the Map with New Data

If you want to update the map with a new frequency dataset (e.g., number of publications, citations, or any other metric), follow these steps:


##### Step 1. Process data in R

Use the provided R script to:

- Load the Excel file exported from `biblioshiny` library (e.g., BiblioshinyReport1.xlsx).

- Convert country names to ISO2 codes.

- Export the updated file in the required format.

  > The full script is available here: update_country_data.R


##### Step 2. Update the Observable Excel file

- Download the `Data_obs.xls` file currently used in your Observable notebook.

- Open the sheet named Sheet6.

- Copy and paste the columns CountryCode and Freq from the R-exported file into columns 1 and 2 of Sheet6.
  
  > Do not modify: 
  > - The red-coded third column in Sheet1
  > - Any sheet name

##### Step 3. Replace the file in Observable
   
- Upload your updated Data_obs.xlsx back to the Observable notebook.

- Run the notebook to regenerate the map with updated data.

  > This method ensures your visualization stays up to date with the latest scientific production metrics, while keeping the internal map logic unchanged.

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

### Citation

To cite this repository in your academic work, teaching, or research:

#### APA style

> Llinás, H. & Rangel, A. (2025). *Global-Scientific-Production-Template* [GitHub repository].
                    GitHub.[https://github.com/hllinas/Global-Scientific-Production-Template/tree/main](https://github.com/hllinas/Global-Scientific-Production-Template/tree/main)
#### BibTeX

```bibtex
@misc{llinas2025timeline,
  author       = {Humberto Llinás, Alexánder Rangel},
  title        = {Global-Scientific-Production-Template},
  year         = {2025},
  howpublished = {\url{https://github.com/usuario/statistical-timeline}},
  note         = {GitHub repository}
}
```
