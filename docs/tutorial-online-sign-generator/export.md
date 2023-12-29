---
sidebar_position: 4
---

# Export

Each sign will have two exported version with and without measurement each svg configuration can be found at:
1. ``SvgOutputDownload`` file.
2. ``SvgMeasurement`` file.

The reason why we use two different format it is because we need both format on `PDF` exported file.

There is extra configuration for Svg with measurement, each sign file should have return extra element with measurement configuration, also there is a lot of path configuration at ``SvgMeasurement`` file to determine how the measurement path is.

## PDF
We have two sign version for reporting pdf, with and without measurement, function that generate that report is same but only use different variable. Function that handle it can be found at `src/utils/autoTable/exportPdf.js`.

We are using ``jspdf`` as main library, signs that exported on the report will be scaled until fit within the predefined size of row x column, all information inside report can easily be found at returning request for each object of sign.


