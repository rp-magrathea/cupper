---
title: Color palettes
---

There's no reason why your **Cupper**-powered pattern library has to be all about functionality. You can include style guide-like information such as color palettes too. The `colors` shortcode makes it easy to exhibit colors and their values together. Just supply a comma-separated list of CSS color values.

```go-html-template
{{</* colors "#111111" "#cccccc" "#ffffff" */>}}
```

The result is a one row strip showing each color supplied in order. The colors for **Cupper** are greyscale:

{{< colors "#111111" "#cccccc" "#ffffff" >}}

{{< note >}}
Note that double quotes around each color value are required. Also, any CSS color value is acceptable, not just hex colors.
{{< /note >}}
