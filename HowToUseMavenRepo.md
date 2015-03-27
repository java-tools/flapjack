In order to use the Maven Repository for flapjack you can just add the following to your pom.xml file.

```
<repositories>
        <repository>
            <id>flapjack-release</id>
            <name>Local Maven repository of releases</name>
            <url>http://flapjack.googlecode.com/svn/mvn-repo/released</url>
        </repository>
        <repository>
            <id>flapjack-snapshot</id>
            <name>Local Maven repository of snapshots</name>
            <url>http://flapjack.googlecode.com/svn/mvn-repo/snapshot</url>
        </repository>
</repositories>
```

### Artifacts ###
| **Maven Identifier** | **Description** |
|:---------------------|:----------------|
| flapjack:flapjack | Core module |
| flapjack:flapjack-annotation | Annotation Mapping module |
| flapjack:flapjack-cobol | Cobol field definition module |