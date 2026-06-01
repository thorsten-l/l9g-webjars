# l9g WebJars

In-house [WebJars](https://www.webjars.org/) for front-end assets that are not (or not conveniently) available on Maven Central, packaged under the `de.l9g.webjars` namespace. They let you serve client-side libraries through Maven/Spring Boot instead of a CDN or a manual copy into `src/main/resources/static`.

This is a multi-module Maven build. The parent (`de.l9g.webjars:webjars-parent`) is an aggregator that hoists the shared encoding, the pinned `maven-jar-plugin`, the OSGi/WebJar manifest entries, and a `release` profile for publishing to Maven Central.

## Modules

| Module | Artifact (`de.l9g.webjars`) | Version | Upstream | License |
|---|---|---|---|---|
| `adminlte-webjar` | `adminlte` | 4.0.0 | [AdminLTE 4](https://adminlte.io) | MIT |
| `jsvectormap-webjar` | `jsvectormap` | 1.5.3 | [jsVectorMap](https://github.com/themustafaomar/jsvectormap) | MIT |
| `source-sans-3-webjar` | `source-sans-3` | 5.0.12 | [@fontsource/source-sans-3](https://fontsource.org/fonts/source-sans-3) | SIL OFL 1.1 |

Each module follows the standard WebJar layout, exposing its assets under:

```
META-INF/resources/webjars/<artifactId>/<version>/...
```

and ships a `webjars-locator.properties` so the version can be resolved at runtime without hard-coding it.

## Requirements

- JDK 17+
- Maven 3.9+

## Building

From this directory (the reactor root):

```bash
# Validate the reactor
mvn validate

# Build and install all WebJars into your local ~/.m2 repository
mvn clean install
```

## Usage

Add the WebJar(s) you need as dependencies:

```xml
<dependency>
  <groupId>de.l9g.webjars</groupId>
  <artifactId>adminlte</artifactId>
  <version>4.0.0</version>
</dependency>
<dependency>
  <groupId>de.l9g.webjars</groupId>
  <artifactId>jsvectormap</artifactId>
  <version>1.5.3</version>
</dependency>
<dependency>
  <groupId>de.l9g.webjars</groupId>
  <artifactId>source-sans-3</artifactId>
  <version>5.0.12</version>
</dependency>
```

### Spring Boot

With `org.webjars:webjars-locator-lite` on the classpath, Spring Boot serves WebJar content from `/webjars/**` and resolves the version automatically, so templates can reference assets without pinning a version:

```html
<link rel="stylesheet" href="/webjars/adminlte/css/adminlte.min.css">
<link rel="stylesheet" href="/webjars/source-sans-3/index.css">
<link rel="stylesheet" href="/webjars/jsvectormap/jsvectormap.min.css">

<script src="/webjars/adminlte/js/adminlte.min.js"></script>
<script src="/webjars/jsvectormap/jsvectormap.min.js"></script>
```

Without the locator, reference the full versioned path, e.g. `/webjars/adminlte/4.0.0/js/adminlte.min.js`.

## Releasing

The parent defines a `release` profile that signs artifacts with GPG and publishes via the Sonatype `central-publishing-maven-plugin`:

```bash
mvn -P release clean deploy
```

This requires:

- A GPG key available to `maven-gpg-plugin`.
- A `<server>` entry with id `ossrh` (a Central Portal token) in your `~/.m2/settings.xml`.

## License

The build itself (this parent POM) is licensed under the [MIT License](https://opensource.org/licenses/MIT). Each bundled library retains its own upstream license as listed in the module table above.
