---
title: Creating a collapsible panel shortcode for Hugo
description: ""
date: 2022-07-10T08:07:48.937Z
preview: creating-collapsible-panel-shortcode-hugo.jpg
draft: true
tags:
  - hugo
lastmod: 2022-07-09T12:04:13.481Z
slug: creating-collapsible-panel-shortcode-hugo
---

I wanted to have a collapsible panel for the blog so that I could use it for hiding optional content like large pieces of code or screenshots, or to provide some extra information.
Most UI frameworks come with a collapsible out-of-the-box:

* Bootstrap's [Collapse](https://getbootstrap.com/docs/4.0/components/collapse/)
* Angular Material's [Expansion panel](https://material.angular.io/components/expansion/overview)
* Element Plus' [Collapse](https://element-plus.org/en-US/component/collapse.html)

The CSS framework this blog is built with -- Bulma -- does not, and none of the Markdown parsers that I have used support it, including [Goldmark](https://github.com/yuin/goldmark/) used by Hugo. So, I decided to make one myself using the `details` element.

[TL;DR](#final-version)

## \<details>

My first instinct was to combine some basic HTML and CSS styling with browser JavaScript for interactivity, but I soon came across something more convenient: the `<details>` element.

From the [HTML spec](https://html.spec.whatwg.org/multipage/interactive-elements.html#the-details-element):
{{< class "is-info" >}}
> The [`details`](https://html.spec.whatwg.org/multipage/interactive-elements.html#the-details-element) element [represents](https://html.spec.whatwg.org/multipage/dom.html#represents) a disclosure widget from which the user can obtain additional information or controls.
{{< /class >}}

It is interactive by default and quite simple to use. Click “Panel hint” to expand the element:
{{< highlightAndPreview "details_default.html" `height="100"` >}}

Adding the open attribute to `details` opens the panel by default:
{{< highlightAndPreview "details_default_open.html" `height="100"` >}}

The aim for this blog is to use as little JavaScript as possible, so having a ready-to-use element, supported by all modern browser was a great gift.

## Hugo Shortcode

A shortcode is a snippet that can be used with Hugo content, they're a special type of template that can be used inside Markdown files.  
An example of a built-in Hugo shortcode is `tweet`:

{{< columns icon="/img/hugo.svg" >}}
```markdown
{{&lt; tweet user=&quot;Jack&quot; id=&quot;20&quot; &gt;}}
```
$$
{{< tweet user="Jack" id="20" >}}
{{< /columns >}}

Read more in the Hugo docs: https://gohugo.io/content-management/shortcodes/.

### Shortcode Definition

Like all Hugo templates, a shortcode is defined by creating an HTML file in the site's or theme's `layouts` directory. The name of the file defines the name of the shortcode, for my custom collapsible shortcode I went with `collapse.html`.

The `tweet` shortcode is a one-liner, fully configured with parameters, but I wanted to be able to embed rich markdown content inside of my collapsible so next to parameters I needed a shortcode that uses an opening and closing tag:

**collapse.html**
```html
<details>
    <summary> Click to extend... </summary>
    {{ .Inner | markdownify | safeHTML}}
</details>
```
<br/>

The `.Inner` variable contains the raw text between the opening and closing shortcode tags, by piping it into `markdownify` and `safeHTML` it will be rendered. 
 
{{< columns icon="/img/hugo.svg" >}}
```markdown
{{&lt; collapse &gt;}}
**Cillum** deserunt voluptate ut duis incididunt in.
{{&lt; /collapse &gt;}}
```
$$
<details class="raw">
    <summary>Click to extend...</summary>
    <b>Cillum</b> deserunt voluptate ut duis incididunt in.
</details>
{{< /columns >}}

### Adding Parameters

I wanted to be able to set the collapsible hint text and also to specify whether the panel should be open on page load. The easiest way to do this with shortcodes is to use named parameters:

```html
{{ $Summary := .Get "summary" | default "Click to extend..." }}
{{ $Open := eq (.Get "open") "true" }}
<details {{ if $Open }}open{{ end }} >
    <summary>{{ $Summary }}</summary>
    {{ .Inner | markdownify | safeHTML}}
</details>
```

Now I could pass the `summary` and `open` parameters to the opening shortcode tag:
{{< columns icon="/img/hugo.svg" >}}
```markdown
{{&lt; collapse summary="Collapse/Extend" open="true" &gt;}}
**Cillum** deserunt voluptate ut duis incididunt in.
{{&lt; /collapse &gt;}}
```
$$
<details class="raw" open>
    <summary>Collapse/Extend</summary>
    <b>Cillum</b> deserunt voluptate ut duis incididunt in.
</details>
{{< /columns >}}

### Final Version

I like having my shortcodes work with both positional and named parameters, so with some tweaks this is what I ended up with:

```html
{{ $Open := false}}
{{ $Summary := .Site.Params.default_spoiler_summary | default "Hidden" }}
{{ if .IsNamedParams }}
    {{ $Summary = .Get "summary" | default $Summary }}
    {{ $Open = eq (.Get "open") "true" }}
{{ else }}
    {{ $Summary = cond (eq (.Get 0) "open") $Summary (.Get 0) | default $Summary }}
    {{ $Open = or (eq (.Get 0) "open") (eq (.Get 1) "open") }}
{{ end }}
<details{{ if $Open }} open{{ end }}>
    <summary>{{ $Summary }}</summary>
    <div>
        {{ .Inner | markdownify | safeHTML }}
    </div>
</details>
```

I find using shortcodes without parameter names cleaner in most cases, and being able to just write 'open' makes fasdd asdfsdf adsfasdfff ds ASD asdasddddddddddddddff

{{< columns icon="" >}}
```markdown
{{&lt; collapse &gt;}}
**Content**
{{&lt; /collapse &gt;}}
```
$$
```markdown
{{&lt; collapse open &gt;}}
**Content**
{{&lt; /collapse &gt;}}
```
$$
```markdown
{{&lt; collapse open "Toggle..." &gt;}}
**Content**
{{&lt; /collapse &gt;}}
```
{{< /columns >}}

{{< columns icon="" >}}
<details class="raw">
    <b>Content</b>
</details>
$$
<details class="raw" open>
    <b>Content</b>
</details>
$$
<details class="raw" open>
    <summary>Toggle...</summary>
    <b>Content</b>
</details>
{{< /columns >}}
