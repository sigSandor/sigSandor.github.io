---
layout: default
title: Home
nav_order: 1
description: "Focusing on Documentation"
---


New (v1.0)
{: .label .label-green }

![new](/assets/new.png){: width="auto" height="auto" }


<button class="btn js-toggle-dark-mode">Toggle Darkmode</button>

<script>
const toggleDarkMode = document.querySelector('.js-toggle-dark-mode');

jtd.addEvent(toggleDarkMode, 'click', function(){
  if (jtd.getTheme() === 'dark') {
    jtd.setTheme('light');
    toggleDarkMode.textContent = 'Preview dark color scheme';
  } else {
    jtd.setTheme('dark');
    toggleDarkMode.textContent = 'Return to the light side';
  }
});
</script>


# Focusing on writing easy-to-read quality documentation
{: .fs-9 }

First, I would like to credit 3 core components that made this project functionable. Github/Github Pages, Jekyll website builder, and the original Template repository is from JustTheDocs. 


{: .fs-6 .fw-300 }

[GitHub Pages][GitHub Pages]{: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Jekyll][Jekyll]{: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Just the Docs][Just the Docs repo]{: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }


#{: .btn .fs-5 .mb-4 .mb-md-0 }

---


[Jekyll]: https://jekyllrb.com
[Markdown]: https://daringfireball.net/projects/markdown/
[Liquid]: https://github.com/Shopify/liquid/wiki
[Front matter]: https://jekyllrb.com/docs/front-matter/
[Jekyll configuration]: https://jekyllrb.com/docs/configuration/
[source file for this page]: https://github.com/just-the-docs/just-the-docs/blob/main/index.md
[Just the Docs Template]: https://just-the-docs.github.io/just-the-docs-template/
[Just the Docs]: https://just-the-docs.com
[Just the Docs repo]: https://github.com/just-the-docs/just-the-docs
[Just the Docs README]: https://github.com/just-the-docs/just-the-docs/blob/main/README.md
[GitHub Pages]: https://pages.github.com/
[Template README]: https://github.com/just-the-docs/just-the-docs-template/blob/main/README.md
[GitHub Pages]: https://pages.github.com/
[customize]: {% link docs/customization.md %}
[use the template]: https://github.com/just-the-docs/just-the-docs-template/generate


