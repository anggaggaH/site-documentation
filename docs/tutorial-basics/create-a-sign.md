---
sidebar_position: 1
---

# Create a Sign

## Create Sign Type
First thing that you should do is [create new sign type](https://api2.bdsamferdsel.no/sign_types/) if doesn't exist. Based documentation sign type is value in hundred between 100 s.d 900
## Create Sub-Sign Type
You can continue with [Create Sub-Sign Type](https://api2.bdsamferdsel.no/sign_sub_types/).

```
{
    "sign_type": 1,
    "colors": *select base color*,
    "font_sizes": *select list of supported font size*,
    "type": "713",
    "name": "713 Vanlig vegviser",
    "svg_file": *uploaded later*,
    "svg_string": *uploaded later*,
    "svg_json": "713",
}
```

*you can comeback to fill **svg_file** and **svg_string** when you successfully generated the sign*.
For the **svg_json** you should follow predefined format, below is example for *701.1* sign:

```
[
    {
        "id": 3,
        "type": "rectangle",
        "background": "trafikkgul",
        "signSubTypeId": 5,
        "elements": [
        {
            "type": "direction",
            "componentName": "TriangleEdge",
            "textContent": "",
            "variant": "left",
            "position": "middle"
        },
        {
            "componentName": "RoadNumber",
            "isDashed": false,
            "position": "top",
            "textContent": "E 0",
            "type": "road-number",
            "variant": "trafikkgrønn"
        },
        {
            "type": "icon",
            "componentName": 213,
            "position": "top"
        },
        {
            "type": "text",
            "componentName": "Text",
            "textContent": "H",
            "variant": "",
            "position": "top"
        },
        {
            "type": "text",
            "componentName": "Text",
            "textContent": "H",
            "variant": "",
            "position": "bottom"
        }
        ]
    },
]
```
- *type* is sign type.
- *componentName* is file name written in CamelCase format that should be same with file name in the source code, but for icon, arrow and symbol it uses **id** of that element type.
- *textContent* is text that will be displayed on that element type.
- *variant* used like theme in road-number element type.

## Create sign File

1. Create a file at `src/components/SignViewer/renderSignTemplate/sign_type.tsx`:

```jsx title="src/components/SignViewer/renderSignTemplate/sign_type.tsx"
import React from 'react';
import SignViewer from '../SignViewer';
import { Element, Structure } from '../../../types/structure.interface';
import { BackgroundColors, Icons, RenderSvgDependencies } from './types';

const signType = (
	scale: number[],
	lines: Structure[],
	icons: Icons,
	bg: BackgroundColors,
	isDownload: boolean,
	isMeasure: boolean,
	_this: SignViewer
) => {
    function getElementsWidthAndOrder(elements: Element[], idxLine: number, roadNumberWidth: number) {
        // this function should returning array of width and ordering elements based on index position
    }
    function _renderSvg(dependencies: RenderSvgDependencies) {
        // this function should return 5 variables
        return {
			renderSvg: elementsResult,              // map of sign elements
			renderSvgM: elementMeasurementResult,   // map of sign elements with measurement
			elementsWidth: elementsWidth,           // map of sign width
			elementsOrder,                          // map of sign elements after order
		};
    }

    // --- Main templating ---
	let totalBaseHeight: number = 0;
	let highestRectWidth: number = 0;
	let renderSvgs: JSX.Element[] = [];
	let renderSvgMs: JSX.Element[] = [];
	let baseHeights: number[] = [];
    lines.forEach((line: Structure, idxLine: number) => {
        // this function will calculate baseHeights, totalBaseHeights, and highestRectWidth

        let renderResult = _renderSvg({
            // returning value from this function on line 101
        })
    });

    // this function should return 5 variables
    return {
		renderSvgs,         // html for regular sign
		renderSvgMs,        // html for sign with measurement
		highestRectWidth,   // highest width of sign
		totalBaseHeight,    // total height of sign
		baseHeights,        // array of base height each of sign
	};
};
export default signType;
```

for more information you can see to one of the sign file in `src/components/SignViewer/renderSignTemplate/`

2. Create a file at `src/components/SignViewer/adjustStructure/sign_type.tsx`:

```jsx title="src/components/SignViewer/adjustStructure/sign_type.tsx"
import React from "react"
import _ from "lodash"
import Context from "../../../Context"
import { Structure } from '../../../types/structure.interface'

function sign_type(structure: Structure[], appContext: React.ContextType<typeof Context>) {
    // this function will return new object elements structure
    // you can order, add/remove and move element structure here
}
export default sign_type

```
for more information you can see to one of the adjusted sign file in `src/components/SignViewer/adjustStructure/`

3. Register above function on index function for each folder after that call that function inside **elementsToRender** → `src/components/SignViewer/SignViewer.tsx`

this is only about creating a sign file, you can't see any effect on UI right now, to do that you should start to configure it.
