---
title: Code blocks
weight: 1
---

Markdown already supports code samples both inline (using single backticks like \`some code here\`) and in blocks. **Cupper** will syntax highlight HTML, CSS, and JavaScript if you provide the correct language in the formulation of the block.

So, this…

{{< highlight markdown >}}
```html
<button aria-pressed="false">toggle me</button>
```
{{< /highlight >}}

…will result in this:

```html
<button aria-pressed="false">toggle me</button>
```

Note that the syntax highlighting uses a greyscale theme. **Cupper** is careful not to use color as part of its own design, because these colors may clash with those of the design being illustrated and discussed.

{{< note >}}
To preserve the wrapping inside code blocks, horizontal scrolling is implemented. To make sure scrolling is keyboard accessible, code blocks are focusable. An `aria-label` is provided to identify the code block to screen reader users.
{{< /note >}}

## Annotated code

**Cupper** offers the ability to highlight and annotate specific parts of your code examples using the `annotatedCode` shortcode. Take an accessible dialog. You may wish to point out key attributes that make that dialog support assistive technologies:

{{< annotatedCode >}}
<div [[[role="dialog"]]] [[[aria-labelledby="dialog-heading"]]]>
  <button [[[aria-label="close"]]]>x</button>
  <h2 [[[id="dialog-heading"]]]>Confirmation</h2>
  <p>Press <strong>Okay</strong> to confirm or <strong>Cancel</strong></p>
  <button>Okay</button>
  <button>Cancel</button>
</div>
{{< /annotatedCode >}}

You mark out the highlighted areas using triple square brackets like so:

```html
{{</* annotatedCode */>}}
<div [[[role="dialog"]]] [[[aria-labelledby="dialog-heading"]]]>
  <button [[[aria-label="close"]]]>x</button>
  <h2 [[[id="dialog-heading"]]]>Confirmation</h2>
  <p>Press <strong>Okay</strong> to confirm or <strong>Cancel</strong></p>
  <button>Okay</button>
  <button>Cancel</button>
</div>
{{</* /annotatedCode */>}}
```

Better still, if you include `numbered="true"`, each highlight is enumerated so you can reference it directly in the ensuing text. If you follow the shortcode directly with an ordered list, the styles match:

{{< annotatedCode numbered="true" >}}
<div [[[role="dialog"]]] [[[aria-labelledby="dialog-heading"]]]>
  <button [[[aria-label="close"]]]>x</button>
  <h2 [[[id="dialog-heading"]]]>Confirmation</h2>
  <p>Press <strong>Okay</strong> to confirm or <strong>Cancel</strong></p>
  <button>Okay</button>
  <button>Cancel</button>
</div>
{{< /annotatedCode >}}

1. The dialog is only announced as a dialog if it takes the `dialog` ARIA role
2. The `aria-labelledby` relationship attribute makes the element carrying the `id` it points to its label
3. The close button uses `aria-label` to provide the text label "close", overriding the text content
4. The heading is used as the dialog's label. The `aria-labelledby` attribute points to its `id`

You just include `numbered="true"` on the opening shortcode tag:

```html
{{</* annotatedCode numbered="true" */>}}
<div [[[role="dialog"]]] [[[aria-labelledby="dialog-heading"]]]>
  <button [[[aria-label="close"]]]>x</button>
  <h2 [[[id="dialog-heading"]]]>Confirmation</h2>
  <p>Press <strong>Okay</strong> to confirm or <strong>Cancel</strong></p>
  <button>Okay</button>
  <button>Cancel</button>
</div>
{{</* /annotatedCode */>}}

1. The dialog is only announced as a dialog if it takes the `dialog` ARIA role
2. The `aria-labelledby` relationship attribute makes the element carrying the `id` it points to its label
3. The close button uses `aria-label` to provide the text label "close", overriding the text content
4. The heading is used as the dialog's label. The `aria-labelledby` attribute points to its `id`
```

### JavaScript example

{{< annotatedCode numbered="true" >}}
/* Enable scrolling by keyboard of code samples */
(function () {
    var codeBlocks = document.querySelectorAll('pre, .code-annotated');

    Array.prototype.forEach.call(codeBlocks, function (block) {
        if (block.querySelector('code')) {
            block.setAttribute([[['role', 'region']]]);
            block.setAttribute([[['aria-label', 'code sample']]]);
            if (block.scrollWidth > block.clientWidth) {
                block.setAttribute('tabindex', '0');
            }
        }
    });
}());
{{< /annotatedCode >}}

1. The `region` role announces the block as a region
2. The `aria-label` describes the kind of content to be expected in the region

{{< note >}}
As you may have noticed, using specified highlights with the `code` shortcode sacrifices syntax highlighting. If you want syntax highlighting you must use the markdown triple back-tick syntax and annotation is not available.
{{< /note >}}
