# nl-core: design tokens

Shared theme settings for every nl- module. Colours, fonts, line height, widths and spacing are set in **Theme settings** and output as `--nl-*` CSS variables on `:root`.

Modules work without nl-core, because every variable has a fallback in their CSS. Install it when you want a theme's look to drive the modules from the theme editor.

## Files

```
snippets/nl-tokens.liquid         outputs the variables and loads the serif and nav fonts
settings_schema.fragment.json     three settings groups: Colors, Typography, Layout and spacing
```

## Install

1. Copy `snippets/nl-tokens.liquid` into your theme's `snippets/` folder.
2. Open your theme's `config/settings_schema.json` and paste the three objects from `settings_schema.fragment.json` into its top-level array, for example just before the last group. Setting IDs are prefixed `nl_`, so they won't clash with the theme's own.
3. In `layout/theme.liquid`, inside `<head>` and before your stylesheets, add:
   ```liquid
   {% render 'nl-tokens' %}
   ```
4. Save, then set the values under **Theme settings › Colors / Typography / Layout and spacing**. The defaults are Shinsei Line's.

## Variables

| Group | Variables |
|---|---|
| Colour | `--nl-color-bg`, `-bg-alt`, `-white`, `-placeholder`, `-card`, `-text`, `-ink`, `-text-mid`, `-text-secondary`, `-text-light`, `-text-ghost`, `-on-dark`, `-rule`, `-border`, `-accent`, `-error` |
| Type | `--nl-font-sans`, `--nl-font-serif`, `--nl-font-serif-weight`, `--nl-font-nav`, `--nl-font-nav-weight`, `--nl-line-height` |
| Layout | `--nl-page-width`, `--nl-text-width`, `--nl-space-xs`, `-sm`, `-md`, `-lg`, `-xl` |
| Motion | `--nl-ease`, `--nl-ease-out` |

## Mapping to an existing theme instead

To make modules follow a theme's existing palette without adding settings, skip the steps above and map variables once in your CSS. For Dawn, which stores colours as RGB triplets:

```css
:root {
  --nl-color-ink: rgb(var(--color-foreground));
  --nl-color-text-mid: rgba(var(--color-foreground), 0.75);
  --nl-color-border: rgba(var(--color-foreground), 0.15);
  --nl-font-sans: var(--font-body-family);
  --nl-font-serif: var(--font-heading-family);
}
```
