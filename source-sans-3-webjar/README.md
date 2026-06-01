# Source Sans 3 (Fontsource) WebJar (de.l9g.webjars)

`@fontsource/source-sans-3` 5.0.12 packaged as a WebJar under the
`de.l9g.webjars` namespace. Resources are served at
`/webjars/source-sans-3/5.0.12/…`. The CSS' relative `./files/…` font URLs
resolve correctly because `index.css` and `files/` are siblings inside
the WebJar.

## Install locally

```bash
mvn install
```

## Use

```xml
<dependency>
    <groupId>de.l9g.webjars</groupId>
    <artifactId>source-sans-3</artifactId>
    <version>5.0.12</version>
</dependency>
```

```html
<link rel="stylesheet" href="/webjars/source-sans-3/5.0.12/index.css"
      media="print" onload="this.media='all'"/>
```

Includes seven subsets (cyrillic, cyrillic-ext, greek, greek-ext, latin,
latin-ext, vietnamese) in both `woff` and `woff2`.
