### Website Information

http://streams.incubator.apache.org is a set of interconnected websites generated
by the maven site plugin.  The front page, this page, and most pages linked in the
top nav of the site are part of incubator-streams-master.

#### Website Content

Pages, diagrams, and other hard-linkable resources are stored throughout the source tree.

#### Markdown

* src/site/markdown

Most HTML pages are generated from markdown.  The maven-site-plugin does this during the site build process.

#### Schemas

* src/main/jsonschema
* src/main/xmlschema

JSON and XML Schemas through-out the project are copied to the web page of their respective modules so they can be 
linked to in other projects.

This allows users to extend the canonical streams schemas incrementally and/or re-use specific fields as they see fit.

#### Resources

* src/main/resources
* src/test/resources

Other resources including .conf and .properties files are copied to the web page of their respective modules so 
they can be linked to across projects and in external projects.

This allows users to import HOCON from modules outside their sphere of control and adapt to changes upstream.

### Website Changes

The project website(s) are hosted by the Apache foundation and updated via SVN.

Currently pushing website changes is a manual process performed by whomever is making the change.

This typically requires checking out the current website from SVN.

    `svn co https://svn.apache.org/repos/infra/websites/production/streams/content`
    `cd content`
    
#### Preparing to publishing a new website version

The instructions below presume:

* you have a shell open in the SVN content directory
* you know the artifactId and version of the repository you want to publish.

If this is a brand new snapshot or release version, you first need to create a directory corresponding to the new version.

> content$ mkdir site/${project.version}
> content$ svn add site/${project.version}
> content$ svn commit -m "svn add site/${project.version}"
    
The first time a specific site is being published for this version, you must create the directory where it will be published.

> content$ mkdir site/${project.version}/${project.artifactId}
> content$ svn add site/${project.version}/${project.artifactId}
> content$ svn commit -m "svn add site/${project.version}/${project.artifactId}"

If you are published over an existing snapshot, you must first remove the existing version and recreate an empty directory.

> content$ rm -rf site/${project.version}/${project.artifactId}
> content$ svn delete site/${project.version}/${project.artifactId}
> content$ svn commit -m "svn delete site/${project.version}/${project.artifactId}"
> content$ mkdir site/${project.version}/${project.artifactId}
> content$ svn add site/${project.version}/${project.artifactId}
> content$ svn commit -m "svn add site/${project.version}/${project.artifactId}"

The folder must exist and be empty for the publish steps to succeed.

Repositories should always be built and published in the following order:

* streams-master
* streams-project
* streams-examples

#### Generating and publishing a new website version
 
The instructions below presume:

* you have a shell open in the root of a project repository
* you know the artifactId and version of the repository you want to publish.

First, ensure that you have local credentials capable of publishing the site.

    <server>
      <id>site.streams.{master|project|examples}</id>
      <username>{your apache ID}</username>
      <privateKey>{absolute path to your private key</privateKey>
      <passphrase>{your private key passphrase}</passphrase>
      <filePermissions>664</filePermissions>
      <directoryPermissions>775</directoryPermissions>
      <configuration></configuration>
    </server>

Next, generate SVG resources for all DOT diagrams in the source tree

> $ for dot in $(find . -name *.dot); do dot -Tsvg $dot -o $dot.svg; done
   
Then, generate the site that will be published
     
> $ mvn clean site:site site:stage
    
At this point you can open target/staging/index.html and do a sanity check on the site you intend to publish.

Finally, publish the site.

> $ mvn scm-publish:publish-scm -Dscmpublish.pubScmUrl=scm:svn:https://svn.apache.org/repos/infra/websites/production/streams/content/site/${project.version}/${project.artifactId}

Note the revision number checked in at the bottom of the maven logs.

You should now be able to access the published site(s) via an absolute URL.

    http://streams.incubator.apache.org/site/${project.version}/${project.artifactId}
    
For example, website documentation from a recent release:

* http://streams.incubator.apache.org/site/0.2-incubating/streams-project/index.html

Some recent snapshots:

* http://streams.incubator.apache.org/site/0.3-incubating-SNAPSHOT/streams-master/index.html
* http://streams.incubator.apache.org/site/0.3-incubating-SNAPSHOT/streams-project/index.html
* http://streams.incubator.apache.org/site/0.2-incubating-SNAPSHOT/streams-examples/index.html

#### Promoting a new website version 

New release or snapshots are immediately published, but visitors to the website won't arrive there from standard links and navigation
until it has been fully promoted.
 
The instructions below presume:

* you have a shell open in the SVN content directory
* you know the artifactId and version of the repository you want to publish.

The convention in place exposes the latest specific site version(s) using redirects maintained in the .htaccess file of project website SVN.

This file can be edited from https://cms.apache.org/streams/

First, click 'Get streams Working Copy'

Next, open .htaccess

If you are promoting sites from all streams repositories simultaneously, the file should end with:

    Redirect /site/latest/ /site/${project.version}
    
If you want to publish sites at different versions across streams repositories, configure as follows:

    Redirect /site/latest/streams-master /site/0.3-incubating-SNAPSHOT/streams-master
    Redirect /site/latest/streams-project /site/0.2-incubating/streams-project
    Redirect /site/latest/streams-examples /site/0.3-incubating-SNAPSHOT/streams-examples

Commit your changes.

Wait a few seconds and click Follow Staging Build.

You should see a new build with a 'Build Successful' message.

Open a new tab and visit http://streams.staging.apache.org for one last check before go-live.

