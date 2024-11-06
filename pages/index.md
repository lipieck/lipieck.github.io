---
layout: default
permalink: /
---

# **About Me**

Hi I am **{{ site.author.name }}** :wave:,<br>
I'm 23 years old, from Poland and I am primarily a developer/analyst. Over time I have built a varied portfolio of skills which I use in my work. In my free time i love to cook and have fun with programming things.

<div class="row">
{% include about/skills.html title="Programming Skills" source=site.data.programming-skills %}
{% include about/skills.html title="Other Skills" source=site.data.other-skills %}
</div>

<div class="row">
{% include about/timeline.html %}
</div>