| Feature               | position: absolute                   | position: fixed                     | position: sticky                    |
|-----------------------|--------------------------------------|-------------------------------------|--------------------------------------|
| Scroll Behavior       | Does not move with content scroll.   | Does not move with content scroll.  | Moves with content until a specified |
|                       |                                      |                                     | scroll position, then becomes fixed.  |
| Relative to           | Relative to the nearest positioned   | Relative to the viewport.           | Relative to the nearest scrollable   |
|                       | ancestor (container).                 |                                     | ancestor (container) or the viewport. |
| Overlapping Content   | May overlap with other elements.      | May overlap with other elements.    | Does not overlap with other elements.|
| Requires Explicit     | Requires explicit positioning using  | Requires explicit positioning using | Requires explicit positioning using  |
| Positioning Values    | `top`, `right`, `bottom`, or `left`.  | `top`, `right`, `bottom`, or `left`. | `top`, `right`, `bottom`, or `left`.  |
| Common Use Cases      | Complex layouts where precise        | Fixed headers or sidebars where     | Headers or elements that need to     |
|                       | positioning is needed within a       | constant visibility is required.    | stick during scrolling.              |
|                       | relative container.                  |                                     |                                      |