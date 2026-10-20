# nl-size-chart: metaobject and metafield definitions

The block reads one product metafield, `nl_modules.size_chart`, which references an `nl_size_chart` entry. That chart lists its sizes and points at `nl_size_row` entries, one per measurement.

One chart can be attached to many products. Measurements are entered **in centimetres only**; the block calculates inches (cm ÷ 2.54, rounded to the nearest half inch).

Create the definitions in this order: rows, then chart, then the product field. (The namespace is `nl_modules` because Shopify requires at least 3 characters; every nl- module shares it.)

## 1. Metaobject definition: `nl_size_row`

**Settings › Custom data › Metaobject definitions › Add definition**

- **Name:** `Size row`. Change the **Type** to **`nl_size_row`**.
- **Fields:**

  | Field name | Key | Type | Validations |
  |---|---|---|---|
  | Measurement | `label` | Single line text › One value | Required. Max 40 characters |
  | Values (cm) | `values_cm` | Decimal › **List of values** | Required. Minimum 0 |

- **Display name:** Measurement
- **Access › Storefronts:** on
- **Save**

## 2. Metaobject definition: `nl_size_chart`

**Add definition** again:

- **Name:** `Size chart`. Change the **Type** to **`nl_size_chart`**.
- **Fields:**

  | Field name | Key | Type | Validations |
  |---|---|---|---|
  | Title | `title` | Single line text › One value | Required |
  | Sizes | `sizes` | Single line text › **List of values** | Required |
  | Rows | `rows` | Metaobject › **Size row** › List of entries | Required |
  | Fit note | `note` | Multi-line text | |
  | Default unit | `default_unit` | Single line text › One value | **Limit to preset choices:** `in`, `cm` |

- **Display name:** Title
- **Access › Storefronts:** on
- **Save**

## 3. Product metafield definition: `nl_modules.size_chart`

**Settings › Custom data › Products › Add definition**

- **Name:** `Size chart`
- **Namespace and key:** **`nl_modules.size_chart`**
- **Type:** Metaobject › **Size chart** › **One entry**
- **Storefronts access:** on
- **Save**

## 4. Add a chart and attach it

1. **Content › Metaobjects › Size row:** add one entry per measurement, with the label and one value per size, **in the same order as the sizes**.
2. **Content › Metaobjects › Size chart:** add an entry. Fill in the title, the sizes in order, the rows (pick the Size row entries), the fit note, and the default unit.
3. **Products ›** open the product **› Metafields › Size chart**, pick the chart, then **Save**.

### Kagemi (Shinsei Line) chart

Sizes: S, M, L, XL. Default unit: `in`.

| Measurement | S | M | L | XL |
|---|---|---|---|---|
| Chest | 56 | 58 | 61 | 64 |
| Shoulder | 50 | 51 | 52 | 53 |
| Length | 119 | 122 | 124 | 127 |
| Sleeve | 60 | 61 | 62 | 64 |

Fit note: "Unisex. Cut with room to layer. Women may prefer one size down. Measurements may vary ±1 cm."

These produce exactly the inch values previously hardcoded (22 / 23 / 24 / 25, 19.5 / 20 / 20.5 / 21, 47 / 48 / 49 / 50, 23.5 / 24 / 24.5 / 25).

## Behaviour

- If `nl_modules.size_chart` is set, the block uses it. Otherwise it builds the chart from its **Fallback chart** settings in the theme editor.
- A row with fewer values than sizes leaves the remaining cells empty. Extra values are shown too, so keep counts equal.
