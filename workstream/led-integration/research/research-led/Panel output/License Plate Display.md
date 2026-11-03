## Concept

License plates should **automatically adjust their font size based on their length** on the 128 × 64 LED matrix panels. Short license plates are displayed larger than long ones to make optimal use of the available space.

## Goal

**All license plates should be displayed consistently, completely, and as large as possible.** The font size adjusts automatically, while the position, color, and overall layout remain unchanged.

The suggested font sizes must be tested on the actual LED matrix before implementation.



## 1. License Plate Lengths

License plates from Switzerland, Germany, France, and Austria must be supported.

| Country     | Short Example | Long Example | Characters  |
| ----------- | ------------- | ------------ | ----------- |
| Switzerland | BS 1          | BS 123456    | 3–8         |
| Germany     | B A 1         | M AB 12345   | 3–8         |
| France      | AB-123-CD     | AB-123-CD    | 7           |
| Austria     | W 1 A         | W 12345 A    | approx. 3–8 |

_Spaces and hyphens are not counted. Special license plates may differ._

## 2. Automatic Font Size

| Characters | Example   | Font Height |
| ---------- | --------- | ----------- |
| 3–4        | BS 1      | 22 px       |
| 5          | BS 123    | 20 px       |
| 6          | BS 1234   | 18 px       |
| 7          | BS 12345  | 16 px       |
| 8          | BS 123456 | 14 px       |


These values are guidelines. The actual rendered width, including spaces and hyphens, determines the final font size.




