# AdminLTE WebJar (de.l9g.webjars)

AdminLTE 4 compiled assets packaged as a WebJar under the `de.l9g.webjars`
namespace. Resources are served at `/webjars/adminlte/4.0.0/…` when used
inside a Spring Boot / Servlet-3-aware container.

## Install locally

```bash
mvn install
```

## Use

```xml
<dependency>
    <groupId>de.l9g.webjars</groupId>
    <artifactId>adminlte</artifactId>
    <version>4.0.0</version>
</dependency>
```

```html
<link rel="stylesheet" href="/webjars/adminlte/4.0.0/css/adminlte.min.css"/>
<script src="/webjars/adminlte/4.0.0/js/adminlte.min.js"></script>
<img src="/webjars/adminlte/4.0.0/assets/img/AdminLTELogo.png"/>
```

## Refreshing the assets

1. In the sibling `AdminLTE/` checkout: `npm install && npm run build`
2. Copy the fresh `dist/{css,js,assets}` over the contents of
   `src/main/resources/META-INF/resources/webjars/adminlte/<version>/`
3. Bump the `<version>` in `pom.xml` (and the directory name above to match)
4. `mvn install`
