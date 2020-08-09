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
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>--block-spacing-after</code></td>
      <td rowspan="10"><code>:root</code></td>
      <td rowspan="10"><code>.Block</code></td>
      <td>Spacing applied after the block container (<code>margin-bottom</code>).</td>
    </tr>
    <tr>
      <td><code>--block-interior-spacing</code></td>
      <td>Spacing applied within the block container (<code>padding</code>).</td>
    </tr>
  </tbody>
</table>