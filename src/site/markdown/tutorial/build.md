## Build streams and streams-examples from source

This tutorial assumes you are using linux or Mac OS X.

### Setup Tools

You'll need the following tools installed in your command line:

* Git
* Java SDK 
* Maven
* Docker

#### Git

  `git -version`
    
| Possible result | Explanation |
|-----------------|-------------|
| bash: git: No such file or directory | You need to install git |
| git version < 2.7 | You should upgrade git for security reasons |
| git version > 2.7 | You are all good |

#### Maven and Java SDK

Run from your command line:

  `mvn -version`

| Possible result | Explanation |
|-----------------|-------------|
| -bash: mvn: command not found | You need to install maven |
| Error: JAVA_HOME is not defined correctly. | You need to install JDK |
| Apache Maven >= 3.2.5+\nJava Version >= 1.7.0u72) | You're all good |
| Apache Maven >= 3.2.5+\nJava Version >= 1.8.0u25) | You're all good |
| Apache Maven < 3.2.5 | You need a newer version of maven |
| Java Version < 1.7.0u72 | You need a newer version of maven |
| Java Version < 1.8.0u25 | You need a newer JDK |

#### Docker

Run from your command line:

  `docker version`

| Possible result | Explanation |
|-----------------|-------------|
| bash: docker: No such file or directory | You need to install docker |
| Client: Version: < 1.0.0 | You need a newer version of docker |
| Server: Version: < 1.0.0 | You need a newer version of docker |
| Client: Version: > 1.0.0\nServer: Version: > 1.0.0 | You are all good |

See [streams-project-index.html](http://streams.incubator.apache.org/site/0.2-incubating/streams-project/index.html "streams-project/index.html") for more information.

### Download Sources

Run from your command line:

> git clone https://github.com/apache/incubator-streams
> git clone https://github.com/apache/incubator-streams-examples
  
### Build Projects

Run from your command line:

> export MAVEN_OPTS="-Xmx2G"
> cd incubator-streams
> mvn clean install -Dmaven.test.skip.exec=true
  
| Possible result | Explanation |
|-----------------|-------------|
| BUILD SUCCESSFUL | You are all good |
| BUILD FAILED | Check yourself |
  
> cd ../incubator-streams-examples
> mvn clean package
  
| Possible result | Explanation |
|-----------------|-------------|
| BUILD SUCCESSFUL | You are all good |
| BUILD FAILED | Check yourself |