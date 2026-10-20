# nl-spec-list: metaobject and metafield definitions

The block reads one product metafield, `nl.specs`, which is a list of `nl_spec` metaobject entries. Create the metaobject definition first, then the metafield that points at it.

These steps use the Shopify admin. Nothing here is created by the theme or the CLI.

## 1. Metaobject definition: `nl_spec`

1. In the Shopify admin, go to **Settings › Custom data**.
2. Under **Metaobject definitions**, click **Add definition**.
3. **Name:** `Spec`. Shopify fills in the **Type** as `spec`. Click the type, change it to **`nl_spec`**, and confirm.
4. Add two fields with **Add field**:

   | Field name | Key | Type | Validations |
   |---|---|---|---|
   | Label | `label` | Single line text › One value | Required. Max 40 characters |
   | Body | `body` | Multi-line text | Required |

   Check that each **Key** matches exactly. Shopify suggests one from the field name, and the block reads `label` and `body`.
5. Set **Display name** to **Label**, so entries are listed as "Design", "Material" and so on.
6. Under **Access**, turn **Storefronts** on. Without this, Liquid can't read the entries.
7. Leave **Publishable** and **Translations** off unless you need them. Click **Save**.

## 2. Product metafield definition: `nl.specs`

1. Go to **Settings › Custom data › Products**, then **Add definition**.
2. **Name:** `Specifications`.
3. **Namespace and key:** click the suggested key and replace it with **`nl.specs`**.
4. **Description** (optional): "Rows shown by the Specifications block."
5. **Type:** **Metaobject**, then select **Spec**, then choose **List of entries**.
6. Under **Access**, make sure **Storefronts** is on.
7. Click **Save**.

## 3. Add the content for a product

1. Go to **Products** and open the product.
2. Scroll to **Metafields**, then click **Specifications**.
3. Choose **Add entry** for each row, filling in **Label** and **Body**. Drag entries to reorder them; the block renders them in this order.
4. Click **Save**.

### Kagemi (Shinsei Line) entries

| Label | Body |
|---|---|
| Design | Structured like a European overcoat. Shaped like a traditional kimono and hakama, with an obi-style belt, pleats and a wide hem. |
| Material | Shell: 100% wool twill, black. Lining: 100% viscose. Imported. |
| Construction | Double-breasted, four-button front with notch lapel. Structured shoulder. Waist panel with self belt. Front pockets. Fully lined. |
| Fit | Unisex. Relaxed through the body and sleeve. Falls below the knee. Model is 6'1" and wears size M. |

## Behaviour

- If `nl.specs` has entries, the block shows them and ignores its Spec row blocks.
- If `nl.specs` is empty or missing, the block shows its Spec row blocks (set in the theme editor). This keeps products without the metafield from rendering an empty list.
- Line breaks in **Body** are kept. HTML is escaped.
