# Portable dataset-binding examples

These examples target MMAS 2.1 and validate against
[`schemas/dataset-binding.schema.json`](../../schemas/dataset-binding.schema.json).

- `aismm-git-markdown.json` — a complete Git snapshot traversed as an MMAS/AISMM tree with a typed GFM block profile;
- `sql-dataset.json` — a parameterized, stably ordered SQL dataset with keyset pagination;
- `mcp-html-harvest.json` — read-only MCP resource enumeration and safe HTML extraction.

They are deliberately different cross-carrier fixtures for the same normative model: logical shape, representation, carrier, access and traversal are declared separately.
