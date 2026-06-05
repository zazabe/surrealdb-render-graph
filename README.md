# SurrealDB Graph Visualizer

Live demo: [https://zazabe.github.io/surrealdb-render-graph/](https://zazabe.github.io/surrealdb-render-graph/)

Static client-side page to load a SurrealDB JSON export, visualize it as a graph, and export high-resolution PNG snapshots.

## Publish on GitHub Pages

1. Push this repo to GitHub.
2. In GitHub, open **Settings → Pages**.
3. Set **Source** to `Deploy from a branch`.
4. Select your branch (usually `main`) and folder `/ (root)`.
5. Save and wait for deployment.
6. Open the URL shown by Pages (for example `https://<user>.github.io/<repo>/`).

No build step is required: `index.html` is the app entrypoint.

## Expected query output shape

The page expects a JSON array mixing node rows and edge rows:

- Node row: `id` and a label field (`label`, `title`, or `text`)
- Edge row: `id`, `in`, `out`, and optional `label`

Example query pattern:

```sql
RETURN array::concat(
    -- Nodes
    (SELECT id, title AS label FROM your_node_table),
    (SELECT id, text AS label FROM another_node_table),

    -- Edges / relations
    (SELECT id, in, out, 'relation_name' AS label FROM your_relation_table)
);
```

## Usage

1. Open the page.
2. Upload your JSON export file.
3. (Optional) run **Optimize Physics Layout**.
4. Set custom width and height.
5. Use **Refresh Export Preview**.
6. Use **Export PNG**.
