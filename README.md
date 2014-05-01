`os-maven-plugin` is a [Maven](http://maven.apache.org/) extension/plugin that generates various useful platform-dependent project properties normalized from `${os.name}` and `${os.arch}`.

`${os.name}` and `${os.arch}` are often subtly different between JVM and operating system versions or they sometimes contain machine-unfriendly characters such as whitespaces.  This plugin tries to remove such fragmentation so that you can determine the current operating system and architecture reliably.

### Generated properties

`os-maven-plugin` detects the name of the current operating system and normalizes it into more generic one.

* `os.detected.name`
  * `aix`
  * `hpux`
  * `os400`
  * `linux`
  * `osx`
  * `freebsd`
  * `openbsd`
  * `netbsd`
  * `sunos`
  * `windows`

`os-maven-plugin` also detects the architecture of the current operating system and normalizes it into more generic one.

* `os.detected.arch`
  * `x86_64`
  * `x86_32`
  * `itanium_64`
  * `sparc_32`
  * `sparc_64`
  * `arm_32`
  * `aarch_64`
  * `ppc_32`
  * `ppc_64`

You can also use the `${os.detected.classifier}` property, which is a shortcut of `${os.detected.name}-${os.detected.arch}`.

### Enabling `os-maven-plugin` on your Maven project

Add the extension to your `pom.xml` like the following:

```xml
<project>
  <build>
    <extensions>
      <plugin>
        <groupId>kr.motd.maven</groupId>
        <artifactId>os-maven-plugin</artifactId>
        <version>1.1.0</version>
      </extension>
    </extensions>
  </build>
</project>

```

### Adding a platform-dependent dependency

Use `${os.detected.classifier}` as the classifier of the dependency:

```xml
<project>
  <dependencies>
    <dependency>
      <groupId>com.example</groupId>
      <artifactId>my-native-library</artifactId>
      <version>1.0.0</version>
      <classifier>${os.detected.classifier}</classifier>
    </dependency>
  </dependencies>
</project>
```

### Generating a platform-dependent dependency

Use `${os.detected.classifier}` as the classifier of the produced JAR:

```xml
<project>
  <build>
    <plugins>
      <plugin>
        <artifactId>maven-jar-plugin</artifactId>
        <configuration>
          <classifier>${os.detected.classifier}</classifier>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

