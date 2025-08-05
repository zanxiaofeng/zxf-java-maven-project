# Maven version Used
- Apache Maven 3.8.7


# Super POM
- maven-model-builder-<your maven version>.jar!/org/apache/maven/model/pom-4.0.0.xml
- https://github.com/apache/maven/blob/maven-3.8.7/maven-model-builder/src/main/resources/org/apache/maven/model/pom-4.0.0.xml


# Effective POM = Super POM + Parent POMs (if any) + Your project POM
- mvn help:effective-pom -Dverbose=true -Doutput=effective-pom.xml


# Plugin maven-compiler-plugin
- mvn compiler:help -Ddetail=true [-Dgoal=compiler:compile]
- https://maven.apache.org/plugins/maven-compiler-plugin/compile-mojo.html


# How plugin maven-compiler-plugin compile java code
## maven-compiler-plugin-3.13.0
- https://github.com/apache/maven-compiler-plugin/tree/maven-compiler-plugin-3.13.0
- public void org.apache.maven.plugin.compiler.AbstractCompilerMojo::execute() throws MojoExecutionException, CompilationFailureException
- org.apache.maven.plugin.compiler.CompilerMojo extends AbstractCompilerMojo
- ** Compile Service **
- org.codehaus.plexus.compiler.Compiler;
- org.codehaus.plexus.compiler.CompilerConfiguration;
- org.codehaus.plexus.compiler.CompilerException;
- org.codehaus.plexus.compiler.CompilerMessage;
- org.codehaus.plexus.compiler.CompilerOutputStyle;
- org.codehaus.plexus.compiler.CompilerResult;
- org.codehaus.plexus.compiler.manager.CompilerManager;
- org.codehaus.plexus.compiler.manager.NoSuchCompilerException;
## maven-compiler-plugin-4.0.0-beta-2
- https://github.com/apache/maven-compiler-plugin/blob/maven-compiler-plugin-4.0.0-beta-2
- public void org.apache.maven.plugin.compiler.AbstractCompilerMojo::execute() throws MojoException
- org.apache.maven.plugin.compiler.CompilerMojo extends AbstractCompilerMojo
- ** Compile Service **
- javax.tools.JavaCompiler
- org.apache.maven.plugin.compiler.ForkedCompiler
- javax.tools.JavaCompiler javax.tools.ToolProvider::getSystemJavaCompiler()
- ServiceLoader<javax.tools.JavaCompiler> ServiceLoader.load(javax.tools.JavaCompiler.class)

# How to set jdk version for a maven project
## Option 1 properties + maven-compiler-plugin
```    
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <!-- For Java 9+(jdk of maven) you might also want to set release -->
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
            <!-- For Java 9+(jdk of maven) you might also want to set release -->
            <release>17</release>
        </configuration>
    </plugin>
```

# Compile parameters of javac
## javac of jdk8
- `-source <release> Provide source compatibility with specified release`
- `-target <release> Generate class files for specific VM version`
## javac of jdk17
- `--source <release>, -source <release> Provide source compatibility with the specified Java SE release. Supported releases: 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17`
- `--target <release>, -target <release> Generate class files suitable for the specified Java SE release. Supported releases: 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17`
- `--release <release> Compile for the specified Java SE release. Supported releases: 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17`
- https://docs.oracle.com/en/java/javase/17/docs/specs/man/javac.html
## javac of jdk22
- `--source <release>, -source <release> Provide source compatibility with the specified Java SE release. Supported releases: 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22`
- `--target <release>, -target <release> Generate class files suitable for the specified Java SE release. Supported releases: 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22`
- `--release <release> Compile for the specified Java SE release. Supported releases: 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22`
- https://docs.oracle.com/en/java/javase/22/docs/specs/man/javac.html