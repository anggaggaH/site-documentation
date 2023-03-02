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
- Default height for each element is **12**
- Space between element from left to right is **4**
- If **road-number** and **icon/symbol** placed side by side distance between them is decreased to **3**

remember that value is just number, we use it as base calculation value to generate final sum in different format *pixel and mm*.

It is also possible to create your sidebar explicitly in `sidebars.js`:

```js title="sidebars.js"
module.exports = {
  tutorialSidebar: [
    'intro',
    // highlight-next-line
    'hello',
    {
      type: 'category',
      label: 'Tutorial',
      items: ['tutorial-basics/create-a-document'],
    },
  ],
};
```
