# How it works

A "plain english" configuration API is defined by a set of variables scoped to `:root` and namespaced to `block`. These variables should be overriden in a `:root` block on a wiki's Special:CSS based on that wiki's needs. Portable "skins" or "themes" can also be created simply from a given `:root` block that can be copied and pasted anywhere.

This stylesheet then worries about how and where to apply these variables, so that end-users don't have to sort through all the different selectors or know actual CSS properties.

If the Blocks variable API does not support a given customization, and if the end-user is familiar with CSS and wants to more granularly customize the Blocks system, they can still write their own CSS by overriding it in Special:CSS.

Furthermore, variables can be made to apply to only one block based on its ID. Every block automatically has an ID generated from its heading. So if a Block section has a heading of "News", variables can be declared in a `#Block-News {  ruleset, which would only be applied to the News section.

In practice, see https://jakanddaxter.fandom.com/wiki/Special:CSS as an example.

Note: `--themed` namespaced variables are native Fandom variables that we're leveraging here for good defaults. These can, however, be replaced. They're typically controlled from the Theme Designer if you'd like to be modular.

## API (WIP)
<table>
  <thead>
    <tr>
      <th>Variable</th>
      <th>Scope</th>
      <th>Selector</th>
      <th>Description</th>
      <th>Default value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>--block-spacing-after</code></td>
      <td rowspan="5"><code>:root</code></td>
      <td rowspan="10"><code>.Block</code></td>
      <td>Spacing applied after the block container (<code>margin-bottom</code>).</td>
      <td><code>1rem</code></td>
    </tr>
    <tr>
      <td><code>--block-interior-spacing</code></td>
      <td>Spacing applied within the block container (<code>padding</code>).</td>
      <td><code>0</code></td>
    </tr>
    <tr>
      <td><code>--block-horizontal-alignment</code></td>
      <td>The horizontal alignment of the Block container's contents, in flexbox terms. So left = <code>flex-start</code>, center = <code>center</code>, right = <code>flex-end</code>, etc.</td>
      <td><code>stretch</code></td>
    </tr>
    <tr>
      <td><code>--block-vertical-alignment</code></td>
      <td>The vertical alignment of the Block container's contents, in flexbox terms (see above).</td>
      <td><code>flex-start</code></td>
    </tr>
    <tr>
      <td><code>--block-background-color</code></td>
      <td>The background color of the Block container (applies to the entire block).</td>
      <td><code>var(--themed-page-background--windows)</code></td>
    </tr>
    <tr>
      <td><code>--block-background-image</code></td>
      <td rowspan="3"><code>:root</code> or <code>#Block-*</code></td>
      <td>The background image of the Block container (applies to the entire block). Note that this is typically used for setting a background for a specific Block, and should thus be set in (scoped to) a specific Block instance's ruleset (e.g. <code>#Block-News</code>).</td>
      <td><code>none</code> (null)</td>
    </tr>
    <tr>
      <td><code>--block-background-size</code></td>
      <td>The size of the background image (only applies if <code>background-image</code> is set, thus same scoping rules).</td>
      <td><code>cover</code></td>
    </tr>
    <tr>
      <td><code>--block-background-position</code></td>
      <td>The position of the background image (see above).</td>
      <td><code>center</code></td>
    </tr>
  </tbody>
</table>