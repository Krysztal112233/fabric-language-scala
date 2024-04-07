# Krysztal's fork of fabric-language-scala

This is a fork of fabric-language-scala,support the newest LTS Scala3 version and bundled Scala Library.

## Why fork?

The number of people who use Scala is very small, but the power of Scala's expressiveness makes the language practically perfect for developing mods.

The original `fabric-language-scala` was unmaintained and the maintainers couldn't spare any more effort to maintain it, so it slowly became unmaintained and non-functional.

Support for Scala3 is, if anything, almost non-existent.

So I decided to fork it and maintain it myself and implement it to be compatible with the original `fabric-language-scala`,named `krysztal-language-scala`.

## NOTE

- This language adaptor will synchronize content upstream as much as possible and will ensure availability as much as possible.
- This language adaptor _**only provide LTS version of Scala3**_

## Bundled libraries

Actually, I think bundled Scala3's standard library is enough.

- scala3-library_3
- scala-library # Required by Scala3

## How to use?

Please notice,the `krysztal-language-scala` only support Scala's `object` now.

### Add dependence

Add those lines to your project's `build.gradle`

```groovy
plugins {
	id 'scala' // Add `scala` plugin for gradle
}

dependencies {
	modImplementation "dev.krysztal:krysztal-language-scala:3.0.0+scala.3.3.3:dev"
  implementation "org.scala-lang:scala3-library_3:3.3.3"
	implementation "org.scala-lang:scala-library:2.13.11"
}
```

### Create entry

Suppose your entry name is `ExampleEntry.scala`

```scala
import net.fabricmc.api.ModInitializer;

object ExampleEntry extends ModInitializer {
    lazy val logger = LoggerFactory.getLogger("KMMO")
    override def onInitialize(): Unit = {
        logger.info("Hi")
    }
}

```

**_ONLY `object` supported now!_**

`class` will be supported later, but `object` is enough.

### Modify `fabric.mod.json`

Suppose your entry in `dev.example`

```json
    ...
 "entrypoints": {
    "main": [
      {
        "adapter": "scala",
        "value": "dev.example.ExampleEntry"
      }
    ],
  },
    ...
```

## Known issues

### unknown invokedynamic bsm: scala/runtime\*

This issues caused by scala's class loading mechanism.

It won't affect almost anything. Ignore it.
