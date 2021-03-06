# Blocks

Blocks is a system of components (or templates) used for creating Main Page designs on Fandom websites. It is replacement for the legacy Portal system. The goal is to be able to easily modify them based on a given wiki's needs, transfer base designs across wikis, and maintain the underlying codebase from a single "source of truth".

Just like any other aspect of <code>fandom-modules</code>, the goal is also to provide full transparency for what's going on "under the hood", remaining easily overridable without being overwhelming for non-developers. To that end, aspects and parts of code for this project are revealed in a "layered" way, such that the code a person is exposed to is only what they need or want to see.

## How it works

A set of "plain english" variables are provided in a <code>:root { }</code> ruleset, which can be changed by end-users and used to create portable "themes" or "skins" that can be added just by copying and pasting the said <code>:root { }</code> block of code. See <code>_example.css</code> as a basic example.

The imported CSS library then worries about how and where to apply these variables, so that end-users don't have to sort through all the different selectors or know actual CSS.

If the Blocks variable system does not support a given customization, and if the end-user is familiar with CSS and wants to more granularly customize the Blocks system, they can still write their own CSS by overriding it in Special:CSS on their wiki.

Furthermore, variables can be made to apply to only one block based on its ID. Every block automatically has an ID generated from its heading. So if a Block section has a heading of "News", variables can be redefined in a <code>#Block-News { }</code> ruleset, which would then only apply to the News section.

In practice, see https://newwikiorder.fandom.com/ as an example.

## API (WIP)

The below table lists all of the CSS custom properties (aka "variables") that compose the Block system (i.e. is the Block API).

<table>
  <thead>
    <tr>
      <th>Variable</th>
      <th>Description</th>
      <th>Default value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th colspan="3">Block container (<code>.Block</code>)</th>
    </tr>
    <tr>
      <td><code>--block-spacing-after</code></td>
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
      <td><code>var(--themed-page-background--windows)</code>*</td>
    </tr>
    <tr>
      <td><code>--block-background-image</code></td>
      <td>The background image of the Block container (applies to the entire block). Note that this is typically used for setting a background for a specific Block, and should thus be set in (scoped to) a specific Block instance's ruleset (e.g. <code>#Block-News</code>).</td>
      <td><code>none</code></td>
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
    <tr>
      <td><code>--block-border</code></td>
      <td>The border of the Block container (applies to the entire block).</td>
      <td><code>none</code></td>
    </tr>
    <tr>
      <td><code>--block-font-family</code></td>
      <td>The font family/font face of the Block. Set to Rubik, Fandom's brand font, by default.</td>
      <td><code>Rubik, sans-serif</code></td>
    </tr>
    <tr>
      <th colspan="3">Block header (heading container) (<code>.Block__header</code>)</th>
    </tr>
    <tr>
      <td><code>--block-header-spacing-after</code></td>
      <td>Spacing applied after the block header (<code>margin-bottom</code>).</td>
      <td><code>1rem</code></td>
    </tr>
    <tr>
      <td><code>--block-header-interior-spacing</code></td>
      <td>Spacing applied within the block header (<code>padding</code>).</td>
      <td><code>1rem</code></td>
    </tr>
    <tr>
      <td><code>--block-header-horizontal-alignment</code></td>
      <td>The horizontal alignment of the content within the header, in flexbox terms.</td>
      <td><code>center</code></td>
    </tr>
    <tr>
      <td><code>--block-header-vertical-alignment</code></td>
      <td>The vertical alignment of the content within the header, in flexbox terms.</td>
      <td><code>center</code></td>
    </tr>
    <tr>
      <td><code>--block-header-background-color</code></td>
      <td>The background color of the header container.</td>
      <td><code>var(--themed-page-background-secondary)</code>*</td>
    </tr>
    <tr>
      <td><code>--block-header-background-image</code></td>
      <td>The background image of the header container. Similar to <code>--block-background-image</code>, this is usually used for individual Block instances.</td>
      <td><code>none</code></td>
    </tr>
    <tr>
      <td><code>--block-header-background-size</code></td>
      <td>The background size of the header container.</td>
      <td><code>cover</code></td>
    </tr>
    <tr>
      <td><code>--block-header-background-position</code></td>
      <td>The background position of the header container.</td>
      <td><code>center</code></td>
    </tr>
    <tr>
      <td><code>--block-header-border</code></td>
      <td>The border of the header container. By default, this applies to all four edges, but a popular option is to only do the bottom edge, which can be done with the hidden variable <code>--block-header-border-bottom</code>, while setting <em>this</em> variable to <code>none</code>.</td>
      <td><code>none</code></td>
    </tr>
    <tr>
      <th colspan="3">Block heading (heading text) (<code>.Block__heading</code>)</th>
    </tr>
    <tr>
      <td><code>--block-heading-font-family</code></td>
      <td>The font family/font face of the heading itself. Only necessary if different from the default block font.</td>
      <td><code>inherit</code></td>
    </tr>
    <tr>
      <td><code>--block-heading-font-size</code></td>
      <td>The font size of the heading.</td>
      <td><code>1rem</code></td>
    </tr>
    <tr>
      <td><code>--block-heading-font-weight</code></td>
      <td>The font weight (light, normal, bold, etc.) of the heading.</td>
      <td><code>bold</code></td>
    </tr>
    <tr>
      <td><code>--block-heading-text-color</code></td>
      <td>The color of the heading text.</td>
      <td><code>var(--themed-text-color)</code>*</td>
    </tr>
    <tr>
      <td><code>--block-heading-text-transform</code></td>
      <td>The transformation of the text, e.g. <code>uppercase</code>, <code>lowercase</code>, etc.</td>
      <td><code>none</code></td>
    </tr>
  </tbody>
</table>

Note that there are additional "secret" variables that can be found in the uncompiled source code (<code>blocks.min.scss</code>). These variables are more granular, but typically rarely need to be changed, and are therefore excluded from this table for readability purposes.

For instance, <code>--block-spacing-after</code> <em>should</em> be all that's needed for adding space around a Block container (i.e. <code>margin</code>). However, there can also be found <code>--block-exterior-spacing-top</code>, <code>right</code>, <code>bottom</code>, and <code>left</code> variables in the source, which can be used as well if needed (for whatever reason). These variables are set to <code>0</code> by default except for <code>--block-exterior-spacing-bottom</code>, which is set to the value of <code>--block-spacing-after</code>. You can sort through the source code to ascertain the specifics of other secret variables.

## Miscellaneous

* `--themed` namespaced variables are native Fandom variables that correspond with values set in the Theme Designer. We're leveraging them here for good defaults. These should not be redefined, but they can be replaced if you don't want to use Theme Designer values.