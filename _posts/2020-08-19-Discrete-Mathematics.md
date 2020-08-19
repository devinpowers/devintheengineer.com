
---

title: " Discrete Mathematics Notes"
date: 2020-08-019


excerpt: "Discrete"

---


# Discrete Mathematics Notes are found here:

[Link to Notes](https://github.com/devinpowers/discrete-mathematics)

{% include base_path %}
{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}
