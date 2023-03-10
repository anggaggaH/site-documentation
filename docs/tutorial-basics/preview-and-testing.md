---
sidebar_position: 3
---

# Preview and Testing

## Preview

### Editor

State that generated from `elementsToRender` function is where our preview is created. Returning function at `src/components/SignViewer/SignViewer.tsx` act as preview in our editor, it also handle:
- Multiple preview when sign is saved/updated/exported.
- State `renderSvgs` which hold all `html` for each element will be combined with default `SVG` html.
- Created base plate `rect` with other `rect` as element that hold `stroke/border`.
- Generated a measurement for each of sign to visualize how height and width sign will be and generate extra small text as description.

```jsx title="src/components/SignViewer/SignViewer.tsx"
  return(
    <svg>
      <rect />                      {/* Base Plate */}
      <rect />                      {/* Base Plate Border */}
      {this.state.renderSvgs}       {/* Render Element */}
      {renderTextSign}              {/* Render Small Text */}
      <div />                       {/* Width Top Measurement */}
      <div />                       {/* Total Height Left Measurement */}
      <div />                       {/* Height of Plate Right Measurement */}

      <SvgOutputDownload />         {/* Sign only For Export */}
      <SvgMeasurement />            {/* Sign with Measurement */}
    </svg>
  )
```

## Testing

You can easily analyze whether the `Sign` is correct or not by looking at the editor results. You can compare with the preview from each of sign documentation. You can see often that some of element are overlapping, element size is different, elements cannot be seen or any miss view. Mostly it came from our initial value or result of calculation for some position is not correct, you can refer to each sign file that located `src/components/SignViewer/renderSignTemplate/sign_type.tsx`. Steps that you can check:
1. Check whether `base height`, `plate height`, `scale` are correct.
2. Check initial X and Y position for each element (setting up breakpoints and start debugging).

if the results of all stages above are correct you can try to export it by clicking `Export Pdf` in left sidebar, but before that you must install **CorelDRAW** so that you can see the export results.

### Exported Sign
