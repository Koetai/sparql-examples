---
title: Koetai SPARQL examples
---

# Koetai SPARQL examples

Community-curated SPARQL example queries spanning multiple life-science
endpoints. Each example is a self-describing Turtle file with the query, a
target endpoint, keywords, and provenance for the contributor.

Contribute your own through the
**[SPARQL desktop](https://koetai.github.io/sparql-desktop/)** — sign in with
ORCID, write or paste a working query, and submit. Curators review the
incoming issues and convert validated ones into the files listed below.

## Examples by endpoint

Each link goes to a per-endpoint page with all curated example queries for
that target (auto-generated from the `.ttl` files by the build).

{% assign all = site.static_files | where_exp: "f", "f.path contains '/examples/'" %}
{% assign ttls = all | where_exp: "f", "f.extname == '.ttl'" %}

{% comment %}
Keep only .ttl files that live in a subfolder under examples/ — this skips
the top-level prefixes.ttl and sparql-examples-ontology.ttl, which aren't
endpoint folders. A file is "in a subfolder" iff the path tail after
"/examples/" contains another '/'.
{% endcomment %}
{% assign in_folders = "" | split: "" %}
{% for f in ttls %}
  {% assign tail = f.path | split: '/examples/' | last %}
  {% if tail contains '/' %}{% assign in_folders = in_folders | push: f %}{% endif %}
{% endfor %}

{% assign by_folder = in_folders | group_by_exp: "f", "f.path | split: '/examples/' | last | split: '/' | first" | sort: "name" %}

{% if in_folders.size == 0 %}
*No examples merged yet — be the first contributor.*
{% else %}{% for group in by_folder %}{% if group.name != "" %}
- [{{ group.name }}](./examples/{{ group.name }}/) — {{ group.items.size }} example{% if group.items.size != 1 %}s{% endif %}
{% endif %}{% endfor %}{% endif %}

## Reference

- Schema: shared [`prefixes.ttl`](./examples/prefixes.ttl) (referenced from
  each example as needed) and
  [`sparql-examples-ontology.ttl`](./examples/sparql-examples-ontology.ttl)
  (defines `spex:`).
- Source: [Koetai/sparql-examples](https://github.com/Koetai/sparql-examples)
  — a fork of
  [sib-swiss/sparql-examples](https://github.com/sib-swiss/sparql-examples),
  curated for multi-endpoint use.
- Sister projects:
  [SPARQL desktop](https://github.com/Koetai/sparql-desktop) (contribution UI) ·
  [Koetai platform](https://github.com/Koetai/koetai-platform) (FAIR endpoint hosting).
