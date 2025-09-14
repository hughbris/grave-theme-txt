# Txt Theme

The **Txt** Theme is for [Grav CMS](http://github.com/getgrav/grav).  This README.md file should be modified to describe the features, installation, configuration, and general usage of this theme.

## Description

Port of Txt by HTML5UP

# Configuring

## Menu Features

### Dropdown Menu

### Menu Text & Icons

### Custom Menu Items

## Source theme conformance

Thanks to some weird workarounds that hopefully don't bring me technical debt (sorry future self!), and not wanting to break any existing implementations, I've added a conformance frontmatter property to contain settings for potentially anything that might be a departure from the source HTML5UP theme.

```yaml
# theme elements that should match the source theme rather than an improved one offered in this Grav theme
conformance:
    fontawesome: true
```

### FontAwesome styles

The source theme comes bundled with a [CSS file for FontAwesome (FA) 5.9.0](https://github.com/hughbris/grav-theme-txt/blob/develop/css/fontawesome-all.min.css) from a bygone era before unfortunate rebrands and shiny new internet brands. And who the hell is maintaining a dribbble account? The chances are that your current networks include some that weren't so much as twinkly ketagenesis in Elon's secret uterus.

> Supporting updated versions of FA has forced a small, inconsequential change to the source txt markup. The `@import` rule at the top of `main.css`, which imports FA's CSS, has been moved to the HTML `<head>` as a stylesheet `<link>`, so that it can be practically overridden. That's because there is no `@unimport` rule in CSS (oh I checked) and a quick search tells me there is no effect on page style rendering.

#### Upgrading FontAwesome

There are two simple methods that have been tested on the demo pages. This will describe upgrading to FontAwesome version 7 (FA7).

First, disable the `fontawesome` conformance setting in your theme configuration:

```yaml
conformance:
    fontawesome: false
```

**Method 1, using shortcodes:** If you intend to use shortcodes on your site — even if you don't use them for FontAwesome icons (which you can) — you can easily configure FA7 through the [shortcode-core plugin](https://github.com/getgrav/grav-plugin-shortcode-core).

Install, enable, and configure `shortcode-core.yaml` and add the following values:

```yaml
fontawesome:
  url: https://cdnjs.cloudflare.com/ajax/libs/font-awesome/7.0.1/css/all.min.css
  v5: true # set your confusion aside
```
Use whichever URL for FA7 styles that you like, local or remote.

Then, to use shortcodes:

```markdown
[fa=bluesky extras=fab,class1,class2 /]
```
_(`class1` and `class2` are just examples of additional classes you might want to add.)_

To use simple HTML in your Twig, go for this kind of markup:

```html
<i class="fab fa-mastodon">
```
_They seem to do OK without the `icon brands` classes._

If you're not into the whole brevity thing, and in cases like the footer of this Txt theme — where there is no shortcode out of the box that will reproduce it — use markup like this in your Twig:

```twig
<a class="icon brands fab fa-x-twitter" href="https://xcancel.com/{{ account }}"><span class="label">XCancel</span></a>
```
_The main difference is the addition of a `fab` attribute. This particular theme layout seems to require retaining the `icon brands` classes._

**Method 2, raw dogging:** Copy (if applicable) and override the Twig block `fa_stylesheet` in your theme's `partials/base.html.twig` template. Note that this is nested within the block called`stylesheets`, so if you are also messing with that, you'll need to make sure you don't blitz it.

```twig
{% block fa_stylesheet %}
    {% style 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/7.0.1/css/all.min.css' priority: 99 %}
{% endblock fa_stylesheet %}
```

Basically, you just need to set a URL to your FA7 CSS resource (local or remote) with an appropriately high priority. Note that we removed the test (`{% set fa_conformance=…`) because we are in YOLO mode.

## Notes

* comment count is hardcoded in blog-preview and heading-metadata partial templates
