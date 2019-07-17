# Code Quality Assurance for Java

Our Java coding standards are based on the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html) and
extendended by generally accepted best practices, e.g., defined by Joshua Bloch's 
[Effective Java](https://www.safaribooksonline.com/library/view/effective-java-3rd/9780134686097).

## QA Tools

To check Java source code according to certain quality standards, typically the tools [Checkstyle](https://checkstyle.org/), [PMD](https://pmd.github.io) and [Spotbugs](https://spotbugs.github.io/) (fka Findbugs) are used. Since each of the three tools focuses on different aspects and uses different means to check code, we recommend to use all of them together. The following files provide configurations for them:

* [Checkstyle configuration](checkstyle.xml)
* [PMD ruleset](pmd.xml)
* Spotbugs (Configuration as explained below [for Eclipse](#executing-qa-tools-during-development))

## Support in IDE (Eclipse)

1. If this is the first time you import the settings in Eclipse, check that your target project is not already imported in Eclipse.
2. Open `Eclipse Preferences` -> `Java` -> `Code Style`.
3. Import the files [eclipse-cleanup.xml](eclipse-cleanup.xml), [eclipse-formatter.xml](eclipse-formatter.xml), and [eclipse-import-order.importorder](eclipse-import-order.importorder) in the GUI dialogs `Clean up`, `Formatter`, and `Organize Imports` respectively.
4. Now copy [org.eclipse.jdt.ui.prefs](org.eclipse.jdt.ui.prefs) to the `.settings` folder of your project.
5. Create a `config` folder in your project that contains all tool configurations, i.e., [checkstyle.xml](checkstyle.xml), [checkstyle-suppression.xml](checkstyle-suppression.xml), [pmd.xml](pmd.xml), and [spotbugs-exclude-filter.xml](spotbugs-exclude-filter.xml).
6. Finally, import the project in Eclipse and follow the next subsection to configure the tool's settings.
7. (Optional) Check in all configuration files in your version control system, e.g., your `config` folder. This will allow your team developers to use the same configurations.

### Executing QA Tools during Development

We recommend to use the lightweight [QA Eclipse Plugin](https://github.com/ChristianWulf/qa-eclipse-plugin) by Christian Wulf. Once configured, it continuously checks your code for your configured rules and checks and highlights violations. It supports **PMD** and **Checkstyle** but unfortunately not Spotbugs (currently). After installing the plugin, it adds two entries to your project's properties, where you can specify the locations of rules and checks. The plugin's webpage gives a detailed explanation on this.

For **Spotbugs** support in Eclipse, we have to use its official plugin. You can download it via the Eclipse Marketplace. Unfortunately this plugin cannot be configured by using a single file. Instead you have to set a few configurations manually. Therefore, right-click on your project and choose *Properties*. There, go to *SpotBugs* and then:
* In the top area, set *analysis effort* to *Maximal*
* In tab *Reporter Configuration*, set *minimum confidence to report* to *Low*
* In tab *Filter files*, under *Exclude filter files*, add the [spotbugs-exclude-filter.xml](spotbugs-exclude-filter.xml) file.

In order to show the violated rules of **PMD**, **Checkstyle**, and **Spotbugs** in Eclipse, you have to open the corresponding views via `Window` -> `Show View` -> `Other`

- `Quality Assurance` -> `Checkstyle Violations` and `PMD Violations`
- `SpotBugs`-> `Bug Explorer`

## Support in Build Tool (Gradle)

To set check our defined coding standards during the build process, we provide a [`build.gradle`](build.gradle) file that can serve as a template for your custom [Gradle](https://gradle.org/) build configuration. It is configured to automatically abort the build process if at least one of the QA tools report an error.
