
Analyze the provided image, which displays a label design intended for printing using ZPL (Zebra Programming Language). Identify each distinct visual element on the label (text fields, boxes, lines, barcodes, QR codes, circles, ellipses, diagonals). For each element detected, extract the following information and format it as a table or a CSV file with these specific columns:

1.  **KIND**: The type of the element. Choose from:
    *   `TEXT`: For any text element.
    *   `BOX`: For rectangular shapes (often drawn with `^GB`). Can also represent horizontal or vertical lines if `WIDTH` or `HEIGHT` is equal to `ITEM_SIZE`.
    *   `BARCODE`: For any standard barcode (like Code 128, EAN, etc., drawn with `^BC`).
    *   `QRCODE`: For QR codes (drawn with `^BQ`).
    *   `DIAGONAL`: For diagonal lines (drawn with `^GD`).
    *   `CIRCLE`: For circles (drawn with `^GC`).
    *   `ELLIPSE`: For ellipses (drawn with `^GE`).
    *   `UNKNOWN`: If the element type doesn't fit the above categories.

2.  **X**: The estimated horizontal coordinate (in pixels or dots) of the element's starting point (typically the top-left corner, assuming the origin (0,0) is the top-left of the label). For `CIRCLE` and `ELLIPSE`, this should still be the top-left of the bounding box containing the shape.
3.  **Y**: The estimated vertical coordinate (in pixels or dots) of the element's starting point (typically the top-left corner, assuming the origin (0,0) is the top-left of the label). For `CIRCLE` and `ELLIPSE`, this should still be the top-left of the bounding box containing the shape.
4.  **ITEM_SIZE**: This value depends on the `KIND`:
    *   For `TEXT`: Estimate the font height (in pixels or dots).
    *   For `BOX`, `DIAGONAL`, `CIRCLE`, `ELLIPSE`: Estimate the line thickness (in pixels or dots).
    *   For `BARCODE`: Estimate the barcode height (in pixels or dots).
    *   For `QRCODE`: Estimate the magnification factor (usually an integer like 2, 3, 4, 5... based on visual size relative to a base module size; use a best guess integer).
5.  **TEXT**:
    *   For `TEXT`, `BARCODE`, `QRCODE`: Extract the actual data/text content encoded in the element.
    *   For other `KIND`s: Leave this field empty or null.
6.  **WIDTH**: The estimated width of the element's bounding box (in pixels or dots).
    *   For `BOX`, `DIAGONAL`, `ELLIPSE`: This is the overall width.
    *   For `CIRCLE`: This is the diameter.
    *   For `TEXT`, `BARCODE`, `QRCODE`: Estimate the width of the entire element.
7.  **HEIGHT**: The estimated height of the element's bounding box (in pixels or dots).
    *   For `BOX`, `DIAGONAL`, `ELLIPSE`: This is the overall height.
    *   For `CIRCLE`: This is the diameter (equal to `WIDTH`).
    *   For `TEXT`, `BARCODE`, `QRCODE`: Estimate the height of the entire element. Note: For `BARCODE`, this might differ from `ITEM_SIZE` if `ITEM_SIZE` specifically refers to module height in ZPL context, while `HEIGHT` is the total visual height. Use total visual height here.
8.  **FONT**:
    *   For `TEXT`: Identify the font identifier if possible (e.g., 'A', '0', or a specific font name if discernible). If not clear leave empty. ZPL often uses single letters or numbers (like 'A' through 'Z', '0' through '9').
    *   For other `KIND`s: Leave empty or null.
9.  **ANGLE**: INTEGER. Estimate the rotation angle of the element. Use one of the following values: `0` (normal), `90` (rotated 90 degrees clockwise), `180` (upside down), `270` (rotated 270 degrees clockwise). Default to `0` if not rotated. For `DIAGONAL`, indicate the slant direction if possible (e.g., `R` for right-leaning '/', `L` for left-leaning '\', based on ZPL's `^GD` command interpretation, otherwise use `0`).

Present the final output as a structured table or a CSV file, where each object represents one element found on the label.

Please also provide the URL with all ZPL commands:
http://api.labelary.com/v1/printers/12dpmm/labels/{WIDTH_IN_INCH}x{HEIGHT_IN_INCH}/0/{ALL_ZPL_COMMANDS}


![Image](https://github.com/user-attachments/assets/19e5be47-3bfb-49d4-b4b6-f1625eff266d)
