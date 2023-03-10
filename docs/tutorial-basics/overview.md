---
sidebar_position: 0
---

# Overview

Before you start with this project you should know **basics of Sign Generator** before you made some changes to the **initial template**.
The goal is for the user can easily make a design for some road sign, instantly see the report/output that contains all configurations of the sign, print the exported sign, and put it in the metal.

Meanwhile, the core concept of this website is that we are manipulating SVG html (rect, path, line) based on some rules in the book and pre-defined calculation.

## Sign documentation

Before you dive more deeper you have to understand rules that **BDS** defined to create each of sign, anything unclear or buggy about the documentation feel free to ask.
1. 500 sign [rules](https://drive.google.com/file/d/1SfsTP_9bAJaSp7Pd3DxioezUsMEb9GPe/view?usp=share_link)
2. 700 sign [rules](https://drive.google.com/file/d/1dMss2_3l9MFvrcL6Fogul3ZxXRkohy4D/view?usp=share_link)
3. Plate height [rules](https://drive.google.com/file/d/1lFjnX2NxB9bhyvs_xdD2jFMMHKnC4oIe/view?usp=share_link)
4. Plate width always rounded next to 100mm

## Sign types

| Arrow | Background | CrossNumber |
|:-----:|:----------:|:-----------:|
| <img src="/img/bds-sign/sign-type/arrow.png" alt="Arrow" width="200" height="200" /> | <img src="/img/bds-sign/sign-type/background.png" alt="Background" width="200" height="200" /> | <img src="/img/bds-sign/sign-type/cross-number.png" alt="CrossNumber" width="200" height="200" /> |

| Dynamic Arrow | Icon / Symbol | Ring Number |
|:-------------:|:-------------:|:-----------:|
| <img src="/img/bds-sign/sign-type/dynamic-arrow.png" alt="Dynamic Arrow" width="200" height="200" /> | <img src="/img/bds-sign/sign-type/icon.png" alt="Icon / Symbol" width="200" height="200" /> | <img src="/img/bds-sign/sign-type/ring-number.png" alt="Ring Number" width="200" height="200" /> |

| Road Number | Text | Triangle Edge |
:-----------:|:----:|:-------------:|
| <img src="/img/bds-sign/sign-type/road-number.png" alt="Road Number" width="200" height="200" /> | <img src="/img/bds-sign/sign-type/text.png" alt="Text" width="200" height="200" /> | <img src="/img/bds-sign/sign-type/triangle-edge.png" alt="Triangle Edge" width="200" height="200" /> |

## Sign status
1. Kladd (*draft*)
2. Revisjon (*revision*)
3. Ferdig, til godkjenning (*done, for approval*)
4. Godkjent (*approved*)
5. Godkjent, klar til print (*approved, ready to print*)
6. Tatt ut til print (*taken out for print*)
7. Ble ikke ordre (*do not order*)

Each of status have *workflow index* that used to maintain sign from designing/creating part until order was finished, for more information you can see [complete list](https://skilt.bdsamferdsel.no/settings/statuses).

## Sign position

Sign position is key value pair inside element object of *sign structure* that define where the elements are placed. we can use either number or string as indexed position, it depends how the signs are and how you would manage it.

1. Use **number** as indexed position (**0, 1, 2, 3, 4**)
<img src="/img/bds-sign/overview/overview-sign-1.png" alt="705.1" width="200" height="200" />

2. Use string as indexed position (**top, middle, bottom**)
<img src="/img/bds-sign/overview/overview-sign-2.png" alt="713" width="200" height="200" />

## Sign color

Sign colors it's different for each sign type, the color of the text will depend on the background selection, it is done to ensure that the used color does not conflict each others. The color output itself is different when we use it in the editor, report, and export. For the export section, we use CMYK -based colors while others use RGB -based colors.

## Sign scale

Scale is used to make sure that Sign **Height**, **Width**, **Space Between Element** are fulfilled the requirement.

| Size | px | mm | Editor |
|:----:|:--:|:--:|:------:|
| 70 |37.79 | 10 | 6/7 |
| 105 |56.69 | 15 | 6/7 |
| 126 |68.03 | 18 | 6/7 |
| 140 |75.59 | 20 | 6/7 |
| 175 |94.48 | 25 | 6/7 |
| 210 |113.38 | 30 | 6/7 |
| 280 |151.18 | 40 | 6/7 |
| 315 |170.07 | 45 | 6/7 |
| 350 |188.97 | 50 | 6/7 |

- *Size* is used as default selection on the editor.
- *px* is default measurement variable to display sign only on editor/website also act as multiplication variable that use to generate real size of sign.
- *mm* is default measurement variable to display sign on report and CorelDraw.
- *Editor* is base scale variable that use to calculate everything on editor/website.
