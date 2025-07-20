# Maven version Used
- Apache Maven 3.8.7


# Super POM
- maven-model-builder-<your maven version>.jar!/org/apache/maven/model/pom-4.0.0.xml
- https://github.com/apache/maven/blob/maven-3.8.7/maven-model-builder/src/main/resources/org/apache/maven/model/pom-4.0.0.xml

# Effective POM = Super POM + Parent POMs (if any) + Your project POM
- mvn help:effective-pom -Doutput=effective-pom.xml


# How to set jdk version for a maven project
## Option 1 properties + maven-compiler-plugin
```    
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <!-- For Java 9+ you might also want to set release -->
        <maven.compiler.release>17</maven.compiler.release>
    </properties>
    
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.13.0</version>
    </plugin>
```
## Option 2 maven-compiler-plugin
```
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.13.0</version>
        <configuration>
            <source>17</source>
            <target>17</target>
            <!-- For Java 9+ you might also want to set release -->
            <release>17</release>
        </configuration>
    </plugin>
```