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

## Examples

{% assign all = site.static_files | where_exp: "f", "f.path contains '/examples/'" %}
{% assign ttls = all | where_exp: "f", "f.extname == '.ttl'" %}
{% assign by_folder = ttls | group_by_exp: "f", "f.path | split: '/' | slice: 2,1 | join: ''" | sort: "name" %}

{% if ttls.size == 0 %}
*No examples merged yet — be the first contributor.*
{% else %}
{% for group in by_folder %}{% if group.name != "" %}
### {{ group.name }}

{% for file in group.items %}- [{{ file.name | remove: ".ttl" | replace: "_", " " }}]({{ file.path | relative_url }})
{% endfor %}
{% endif %}{% endfor %}
{% endif %}

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
