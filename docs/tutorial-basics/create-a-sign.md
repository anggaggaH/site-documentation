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

## Add **Sub-Sign Type** object [here](https://api2.bdsamferdsel.no/sign_sub_types/).

Add **Markdown or React** files to `src/pages` to create a **standalone page**:

- `src/pages/index.js` → `localhost:3000/`
- `src/pages/foo.md` → `localhost:3000/foo`
- `src/pages/foo/bar.js` → `localhost:3000/foo/bar`

## Create your first React Page

Create a file at `src/pages/my-react-page.js`:

```jsx title="src/pages/my-react-page.js"
import React from 'react';
import Layout from '@theme/Layout';

export default function MyReactPage() {
	return (
		<Layout>
			<h1>My React page</h1>
			<p>This is a React page</p>
		</Layout>
	);
}
```

A new page is now available at [http://localhost:3000/my-react-page](http://localhost:3000/my-react-page).

## Create your first Markdown Page

Create a file at `src/pages/my-markdown-page.md`:

```mdx title="src/pages/my-markdown-page.md"
# My Markdown page

This is a Markdown page
```

A new page is now available at [http://localhost:3000/my-markdown-page](http://localhost:3000/my-markdown-page).
