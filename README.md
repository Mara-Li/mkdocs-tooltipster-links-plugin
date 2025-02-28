:warning: THIS REPO IS NOW ARCHIVED
**PLEASE USE [TOOLTIPS INTERNAL LINKS](https://github.com/ObsidianPublisher/tooltips-internal-link) INSTEAD**


_Fork of midnightprioriem/mkdocs-tooltipster-links-plugin_

# mkdocs-tooltipster-links-plugin

An MkDocs plugin that adds tooltips to preview the content of page links using tooltipster

![demo](docs/mkdocs_tooltipster_links_demo.gif)

## Setup

### Install the Plugin

Install the plugin using pip:

`pip install mkdocs-preview-links-plugin`

Activate the plugin in `mkdocs.yml`:
```yaml
plugins:
  - search
  - tooltipster-links
```

> **Note:** If you have no `plugins` entry in your config file yet, you'll likely also want to add the `search` plugin. MkDocs enables it by default if there is no `plugins` entry set, but now you have to enable it explicitly.

More information about plugins in the [MkDocs documentation][mkdocs-plugins].

### Install Tooltipster

Please reference [Tooltipster's getting started guide](http://iamceege.github.io/tooltipster/#getting-started) for additional installation instructions.

Download Tooltipster and add the css and javascript to `mkdocs.yml`:

```yml
extra_css:
  - css/tooltipster.bundle.min.css

extra_javascript:
  - js/tooltipster.bundle.js  
```

Create custom directory and `main.html` file for overriding the `extra_head` template block

```sh
mkdir theme
touch theme/main.html
```

Add the following to `main.html`:
```html
{% extends "base.html" %}

{% block extrahead %}
        <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
        <script>
                $(document).ready(function() {
                    $('.link-tooltip').tooltipster();
                });
        </script>
{% endblock %}
```
Add the custom directory to `mkdocs.yml`:
```yml
theme:
  name: mkdocs
  custom_dir: theme
```

Add additonal css to the site (either in a new css file or existing one):
```css
.tooltipster-base {
    max-width: 50%;
}
.tooltipster-content img.wikilink {
    max-width: 10%;
}
.tooltip_templates {
    display: none;
}
```

## Usage
Once configured property, tooltips-links should create tooltips automagically!

The plugin is not compatible with `navigation.instant` in Material Theme. For this theme, some styling are disponible in the [docs/material.css](docs/material.css) file.

### Custom configuration
In you config file to add compatibility for these plugins :
- [mkdocs callouts](https://github.com/sondregronas/mkdocs-callouts)
- [mkdocs custom tags attributes](https://github.com/Mara-Li/mkdocs-custom-tags-attributes)

Just edit your config file and add the following:
```yml
plugins:
  - search
  - tooltipster-links:
      callouts: true
      custom-attributes: 'assets/css/custom_attributes.css'
```

Moreover, you can configure the max characters limits and the characters used after truncate (400 used by default):

```yml
plugins:
  - search
  - tooltipster-links:
      max-characters: 400 #use 0 or 1 for no limit
      truncate-characters: '...'
```

## See Also

More information about templates [here][mkdocs-template].

More information about blocks [here][mkdocs-block].

[mkdocs-plugins]: http://www.mkdocs.org/user-guide/plugins/
[mkdocs-template]: https://www.mkdocs.org/user-guide/custom-themes/#template-variables
[mkdocs-block]: https://www.mkdocs.org/user-guide/styling-your-docs/#overriding-template-blocks
