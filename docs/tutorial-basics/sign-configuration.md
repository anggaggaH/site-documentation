---
sidebar_position: 2
---

# Sign Configuration

Please grab your ☕ and tight your seat before start this section.

## Understanding scale

<img src="/img/bds-sign/sign-configuration/understanding-scale.png" alt="701.1" width="" height="" />

as you can see above that **sign** have a certain height value, there is also value that defining space between element. Based on image above we can have a summary:

- Total height of sign is **71**
- Height of sign if they only have 1 line of position is **19**
- Height of sign is **33** if they have multiple line of position
- Default height for each element is **12**, except text is **7**
- Space between element from left to right is **4**
- If **road-number** and **icon/symbol** placed side by side distance between them is decreased to **3**

remember that we use that value as base calculation to generate final sum in different format _pixel and mm_ based [scale](https://doc.anggahermawan.com/docs/tutorial-basics/overview#sign-scale) here. You can find the function that handle it below here.

```jsx title="/src/components/Helper/getCurrentScale.ts"
export function getCurrentScale() {
	return { arrScales, arrScales5602, rectHeights, additionalHeights, svgHeight, realValue };
}
```

## Sign Plate

### Height

Height of plate should following rules as [documentation](https://doc.anggahermawan.com/docs/tutorial-basics/overview#sign-documentation), if the height somehow doesn't exist in the list then it should rounded next to available plate height.

```jsx title="/src/components/Helper/getNearestPlate.ts"
export function getNearest() {
	return choosenPlate;
}
```

### Width

Width of plate should rounded to next 100mm

## Render
This function will try to get current scale based on font size and distribute to `Sign File` that we create before
```jsx title="/src/components/SignViewer/SignViewer.tsx"
export function elementsToRender() {
  //...

  let { scale, structure } = this.props;
  if (!isDownload) {
	  scale = this.state.resolutionScale;
  }

  const scales: Scale = this.handleChangeScale(scale, isDownload!, !!isMeasure);
  const lines = this.adjustStructure(structure);
  const { newScale, newScales } = scales;

  let sign: ISignRender;
  if (signSubTypeNum) {
    sign = renderSignTemplate.sign560_1(newScale, lines, icons, bg, !!isDownload, !!isMeasure, this);
  }

  //...

  const { renderSvgs, renderSvgMs, highestRectWidth, totalBaseHeight, baseHeights } = sign;

  this.setState({
    renderSvg: renderSvgs,
    renderSvgM: renderSvgMs,
    rectWidth: highestRectWidth,
    baseHeight: totalBaseHeight,
    baseHeights: baseHeights,
    realScales: newScale,
	});
}
```
