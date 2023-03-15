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

[Scale](https://doc.anggahermawan.com/docs/tutorial-online-sign-generator/overview#sign-scale) is a variable that is used as the basis of calculations to determine width and height when the sign is in the editor and when exported. Available in two different format _pixel and mm_.

You can find the function that handle it below here.

```jsx title="/src/components/Helper/getCurrentScale.ts"
export function getCurrentScale() {
	return { arrScales, arrScales5602, rectHeights, additionalHeights, svgHeight, realValue };
}
```

## Element

### Text
Height of the text element is **7**, but set to **12** to automatically give space at the top and bottom of the text itself, the reason is we minimize the effort for positioning the element on the vertical way, but it will cost to inconsistent font size. Standard font size itself around **10.xx**. Text element was made by ``Opentype.js`` with pre-defined config like font type, font size and fill color.

### Road Number
The height of the road number element is fixed at **12**, its width is dynamic and is based on how long the text is. The street number element has been created by joining several ``rect`` or ``path`` html elements with a ``text element``. There is some style/variant for definition of base color and border style.

### Symbol and Icon
The height of the road number element is fixed at **12**, however their existence is limited to some type of sign. ``Symbol`` and ``Icon`` file will be uploaded by admin, so we don't need to create it from scratch.

### Triangle Edge
Until this documentation was published only sign ``713`` and ``729`` that using this element. Each type of sign have different characteristic of the ``triangle`` element.
1. ``729`` have more simple configuration, it has different width for each font size, though that it only contains multiple path to create triangle from two perspective.
2. ``713`` have more complexity, it is because the triangle should have rounded edge in the middle of triangle point. Built from single complicated path and transformed into to some perspective view.

## Sign Plate

### Height

Height of plate should following rules as [documentation](https://doc.anggahermawan.com/docs/tutorial-online-sign-generator/overview#sign-documentation), if the height somehow doesn't exist in the list then it should rounded next to available plate height.

```jsx title="/src/components/Helper/getNearestPlate.ts"
export function getNearest() {
	return choosenPlate;
}
```

### Width

Width of plate should rounded next to 100mm.

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
    sign = renderSignTemplate.signSign_Type(newScale, lines, icons, bg, !!isDownload, !!isMeasure, this);
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

## Example

If we choose a `701.1 sign` based this [image](https://doc.anggahermawan.com/docs/tutorial-online-sign-generator/overview#understanding-scale) with `font size = 175` then value that we defined for each sign should be:
1. Height is `[33, 19, 19] * 25` = `1805mm`.
- `33 * 25mm` = 825mm **Plate Height 825 is not exist** so it should be rounded next to **855**
- `19 * 25mm` = 475mm
- `19 * 25mm` = 475mm

2. Width is dynamic value but it should be `highestWidth * 25mm` = `Xmm` the result should be rounded next to `100mm`.
3. Default Scale is `94.48` if plate height is adjusted then we have new `scale of height`.

## Miscellaneous
1. All sign except 729 have extra 10mm width on left-right, for the calculation already implemented on each sign file.

