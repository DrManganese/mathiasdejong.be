---
title: Build, Deploy and Host a Static Hugo Site on AWS Amplify
date: 2022-06-26T17:16:50.758Z
draft: false
slug: build-deploy-host-static-hugo-site-aws-amplify
description: Do irure labore duis ipsum id sit incididunt Lorem dolor labore qui est dolore
  dolor.#
tags:
  - aws
  - hugo
lastmod: 2022-07-06T19:29:40.242Z
preview: preview.png
---

{{< collapse "This is my summary..." open >}}
Cillum qui exercitation et minim exercitation veniam mollit cillum irure pariatur consequat aute. Ullamco adipisicing officia ipsum occaecat deserunt commodo officia cillum esse sunt consequat labore velit. Duis nulla eiusmod ex in occaecat do id eiusmod consequat esse aliquip tempor id. Nulla ullamco dolor veniam excepteur velit. Sunt do magna aute non sunt aliqua enim irure pariatur proident amet.
{{< figure src="https://picsum.photos/536/354" title="Random picsum placeholder" >}}
{{</ collapse >}}

{{< collapse hint="Some sample PHP code..." open="true" >}}
  ```php
$var = "This is my variable";
```
{{</ collapse >}}

{{< collapse "This is my other summary..." >}}
{{< collapse "This is my other summary..." >}}
adsfdfsdf
{{</ collapse >}}
{{</ collapse >}}

Nulla incididunt veniam irure eu. Anim magna id ipsum adipisicing nostrud excepteur mollit ea officia. Est cupidatat laboris esse eiusmod consectetur deserunt irure ad eu aute dolor consequat sint aliqua. Mollit ad culpa adipisicing est aliqua sint eiusmod aliquip nulla in ea eu. Anim commodo laboris Lorem culpa enim. Laborum adipisicing fugiat reprehenderit duis adipisicing nostrud duis. Cillum dolor est culpa eu ea nulla incididunt duis Lorem et deserunt aliqua cillum sunt.

Et duis aliqua proident culpa fugiat excepteur consectetur mollit Lorem culpa minim. Voluptate ea tempor officia labore laborum elit ullamco elit est qui ea ex minim laborum. Esse veniam elit enim Lorem et nisi velit. Nisi qui deserunt cillum nisi ad. Dolor ut adipisicing incididunt veniam proident nisi et sint in. Ea incididunt quis officia commodo occaecat elit dolore eu duis. Magna quis Lorem ullamco officia.

{{< highlight Scala >}}
val greeting = "Hello, world!"
println(greeting.reverse)
{{< /highlight >}}

Fugiat dolor consectetur reprehenderit do ea. Occaecat consectetur commodo irure sit voluptate et est. Est laborum qui et elit minim ad quis commodo nisi aliquip sint. Nisi labore do quis proident nulla velit dolor cupidatat. Proident sint veniam sunt nulla Lorem velit laboris. Est ut pariatur laboris dolor occaecat culpa quis incididunt duis minim tempor irure ipsum sint.

A narrow table styled with bulma and highlighted using a custom shortcode:
{{< table "table center" 2 >}}
| Column 1 | Column 2 |
|----------|----------|
| 1 | Value 1 |
| 2 | Value 2 |
| 3 | Value 3 |
{{</ table >}}
Markdown:

```markdown
{{</* table "table center" 2 */>}}
| Column 1 | Column 2 |
|----------|----------|
| 1 | Value 1 |
| 2 | Value 2 |
| 3 | Value 3 |
{{</* /table */>}}
```

<br/>

Shortcode:

```html
{{ $htmlTable := .Inner | markdownify }} {{ $class := .Get 0 }} {{ $highlight :=
.Get 1 }} {{ $old := "
<table>
  " }} {{ $new := printf "<table class=\"%s\">" $class }} {{ $htmlTable :=
  replace $htmlTable $old $new }} {{ if $highlight }} {{ template "highlightRow"
  (dict "tbl" $htmlTable "i" $highlight) }} {{ else }} {{ $htmlTable | safeHTML
  }} {{ end }} {{ define "highlightRow" }} {{ $htmlTable := replace .tbl "\n" ""
  }} {{ $old := index (findRE "
  <tr>
    <td>.*?</td>
  </tr>
  " (replace $htmlTable "\n" "")) (sub .i 1) }} {{ $new := replace $old "
  <tr>
    " `
  </tr>
  <tr class="is-selected">
    `}} {{ replace $htmlTable $old $new | safeHTML }} {{ end }}
  </tr>
</table>
```

A wide table that stretches to fit the whole parent container:
| Column 1 | Column 2 |
|----------|----------|
| 1 | Value 1 |
| 2 | Value 2 |
| 3 | Value 3 |

Ut excepteur aliquip elit do sunt. Amet ullamco ullamco non dolore dolore Lorem voluptate aliquip. Aute non enim duis id ad culpa. Deserunt adipisicing minim dolor elit nisi culpa consectetur eiusmod fugiat mollit nostrud do. Do est quis est officia ut eiusmod. Officia nisi eu commodo cillum ex sunt eiusmod occaecat labore minim et Lorem enim excepteur.


{{< columns icon="play">}}
| Column 1 | Column 2 |
|----------|----------|
| 1 | Value 1 |
| 2 | Value 2 |
| 3 | Value 3 |
$$
| Column 1 | Column 2 |
|----------|----------|
| 1 | Value 1 |
| 2 | Value 2 |
| 3 | Value 3 |
{{< /columns >}}