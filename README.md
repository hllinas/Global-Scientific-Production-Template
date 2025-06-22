# Global-Scientific-Production-Template

### Includes Log Coloring, 1:110m Scale, and Labels

This interactive map is inspired by the original work *CountrySciProd Project* by [AlexanderRV22](https://github.com/Alex-rv150/CountrySciProud), which offers a global overview of **scientific production** through visual analytics. Building on that foundation, this version incorporates enhancements such as:

- Logarithmic color scale.
- 1:110m small scale projection.
- Dynamic country labels displaying names and frequencies.

Designed for researchers, educators, and policymakers, this tool allows users to explore how different countries contribute to scientific research. The visualization supports deeper insights into scientific output worldwide, and the code can be easily modified to reflect custom frequency data or labeling preferences.

View the full [here](https://observablehq.com/d/ec528de5c6f1cd3d). 

![image](https://github.com/user-attachments/assets/4ebefd27-c07e-4663-9a29-d71cf42384af)

### Color Options for the Map
This section provides a collection of color scale combinations that you can apply to the Global Scientific Production Template. These color interpolators can be used to highlight scientific production frequencies in different styles, helping tailor the visual experience to your goals.

### Usage
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

### Available Color Interpolators
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
