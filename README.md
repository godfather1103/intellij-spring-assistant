![Version](https://img.shields.io/jetbrains/plugin/v/18622-spring-initializr-and-assistant)
![Downloads](https://img.shields.io/jetbrains/plugin/d/18622-spring-initializr-and-assistant)
![Rating](https://img.shields.io/jetbrains/plugin/r/rating/18622-spring-initializr-and-assistant)
<!-- Plugin description -->
Assist in Spring application development - Adds support for start initializr, autocomplete Spring Boot/Cloud configuration key/value, Spring reference configuration, Spring metadata documentation.(Support: Java, Kotlin, application.yml and bootstrap.properties)

---
## Features:
### Spring Intilializr
1. Allows you to bootstrap new project & new module using `File -> New -> Project -> Spring Assistant` & `File -> New -> Module -> Spring Assistant`
   wizards. Looks & Feel resembles Intellij Ultimate, but with less bells & whistles

<a> <img alt="Spring Intilializr in action" width="300" src="https://github.com/eltonsandre/intellij-spring-assistant/blob/main/demo/initializr.gif?raw=true" /> </a>

### Autocomplete configuration properties

1. Autocompletion of the configuration properties in your `yaml`/`properties` files based on the spring boot's autoconfiguration jars are present in
   the classpath
2. Auto-completion of the configuration properties in your `yaml`/`properties` files if you have classes annotated with `@ConfigurationProperties`
   , [if your build is properly configured](#setup-for-showing-configurationproperties-as-suggestions-within-current-module)
3. Short form search & search for element deep within is also supported. i.e, `sp.d` will show you `spring.data`, `spring.datasource`, also, `port`
   would show `server.port` as a suggestion
4. Quick documentation for groups & properties (not all groups & properties will have documentation, depends on whether the original author specified
   documentation or not for any given element)

<a> <img alt="Autocomplete in action" width="300" src="https://github.com/eltonsandre/intellij-spring-assistant/blob/main/demo/autocomplete-config.gif?raw=true" /> </a>

### Go to configuration properties

1. Ctrl+click to go to property or code

<a> <img alt="Goto in action" width="300" src="https://github.com/eltonsandre/intellij-spring-assistant/blob/main/demo/link-config.gif?raw=true" /> </a>

## Usage

---
Assuming that you have Spring boot's autoconfiguration jars are present in the classpath, this plugin will automatically allows you to autocomplete
properties as suggestions in all your `yml` files

Suggestions would appear as soon as you type/press `CTRL+SPACE`.

Short form suggestions are also supported such as, `sp.d` will show you `spring.data`, `spring.datasource`, e.t.c as suggestions that make your typing
faster

In addition to libraries in the classpath, the plugin also allows you to have your own `@ConfigurationProperties` available as suggestions in all
your `yml` files.

For this to work, you need to ensure the following steps are followed for your project/module

### Setup for showing ConfigurationProperties as suggestions within current module

1. Make sure `Enable annotation processing` is checked under `Settings > Build, Execution & Deployment > Compiler > Annotation Processors`
2. Make sure you add the following changes to your project

#### *For Gradle*

Add the following build configuration. You can use the [propdeps-plugin](https://github.com/spring-gradle-plugins/propdeps-plugin) for `optional`
scope (as we dont need `spring-boot-configuration-processor` as a dependency in the generated jar/war)

```groovy
dependencies {
    optional 'org.springframework.boot:spring-boot-configuration-processor'
}

compileJava.dependsOn(processResources)
```

#### *For Maven*

```xml

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
```

3. (**OPTIONAL**) If intellij is generating build artfacts to `output` directory instead of gradle's default `build` directory, then you may need
   to `File | Settings | Build, Execution, Deployment | Build Tools | Gradle | Runner => Delegate IDE build/run actions to gradle` & restart the IDE.
   This will ensure that gradle plugin generates metadata & Intellij is pointing to it

> If you want to look at a sample project, look inside [samples](https://github.com/eltonsandre/intellij-spring-assistant/tree/main/samples) directory where the above setup is done. These samples allow properties from `@ConfigurationProperties` to be shown as suggestions

---

### This tool is free for personal and commercial usage. [Donations](https://www.paypal.com/donate/?business=CZ9QNZ67X6RPA&no_recurring=0&item_name=Intellij+Spring+Intilializr+%26+assistant%3A%0AThis+tool+is+free+for+personal+and+commercial+usage.+Donations+are+very+welcome+though&currency_code=USD) are very welcome though.

<!-- Plugin description end -->

---
⚠️ **IMPORTANT**

> After changing your custom `@ConfigurationProperties` files, suggestions would be refreshed only after you trigger the build explicitly using keyboard (`Ctrl+F9`)/UI

### Known behaviour in ambiguous cases

> 1. If two groups from different auto configurations conflict with each other, the documentation for the group picked is random & undefined
> 2. If a group & property represent the depth, the behaviour of the plugin is undefined.

## Installation (in 3 easy steps)

To install the plugin open your editor (IntelliJ) and hit:

1. `File > Settings > Plugins` and click on the `Browse repositories` button.
2. Look for `Spring Assistant` the right click and select `Download plugin`.
3. Finally hit the `Apply` button, agree to restart your IDE and you're all done!

Feel free to let me know what else you want added via the [issues](https://github.com/eltonsandre/intellij-spring-assistant/issues)

## Changelog

See [here](CHANGELOG.md)


---

#### This project is a  [Spring Assistant - IntelliJ Plugin](https://github.com/1tontech/intellij-spring-assistant) fork by @1tontech

**why this fork?**

_The idea is to carry out more constant maintenance and additions of new features_

