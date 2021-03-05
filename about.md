---
layout: page
title: About
permalink: /about/
---

CHS Robotics Club is the robotics club at Coronado High school participating in the First Robotics Competition.

Current officers are:

|                            Name | Position       |
|--------------------------------:|----------------|
|      {{site.members.president}} | President      |
| {{site.members.vice_president}} | Vice President |
{% for officer in site.members.officers %}|{{officer}}|Officer|
{% endfor %}{% for other in site.members.other %}|{{other}}|Other|
{% endfor %}

This site was made with [Jekyll]{:target="_blank"} using the [Minima]{:target="_blank"} theme.

It uses [FontAwesome]{:target="_blank"} for the external link icons: <i class="fas fa-external-link-alt"></i>.

This page is hosted with [GitHub pages]{:target="_blank"} and is [open source][GitHub Repo]{:target="_blank"}.

[Jekyll]:https://jekyllrb.com/
[Minima]:https://github.com/jekyll/minima
[FontAwesome]:https://fontawesome.com/
[GitHub pages]:https://pages.github.com/
[GitHub Repo]:https://github.com/CHS-Robotics-Club/CHS-Robotics-Club.github.io