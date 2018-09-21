# Code Quality Assurance for Java

Our Java coding standards are based on the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html) and
extendended by generally accepted best practices, e.g., defined by Joshua Bloch's 
[Effective Java](https://www.safaribooksonline.com/library/view/effective-java-3rd/9780134686097).

## QA Tools

To check Java source code according to certain quality standards, typically the tools [Checkstyle](https://checkstyle.org/), [PMD](https://pmd.github.io) and [Spotbugs](https://spotbugs.github.io/) (fka Findbugs) are used. Since each of the three tools focuses on different aspects and uses different means to check code, we recommend to use all of them together. The following files provide configurations for them:

* [Checkstyle configuration](checkstyle.xml)
* [PMD ruleset](pmd.xml) (**Work in Progress**)
* **TODO** Spotbugs

## Support in IDE (Eclipse)

* **TODO** How to configure Formatter etc. 

### Executing QA Tools during Development

We recommend to use the lightweight [QA Eclipse Plugin](https://github.com/ChristianWulf/qa-eclipse-plugin) by Christian Wulf. Once configured, it continuously checks your code for your configured rules and checks and highlights violations. It supports PMD and Checkstyle but unfortunately not Spotbugs (currently). After installing the plugin, it adds two entries to your project's properties, where you can specify the locations of rules and checks. The plugin's webpage gives a detailed explanation on this.

* **TODO** Spotbugs

## Support in Build Tool (Gradle)

* **TODO** How to execute qa tools (to simply save/print results)
* **TODO** How to set and check for thresholds of violations
