### Create a folder to hold streams configuration files

Pick a place on your file system that's easy to remember and reference with an absolution path.

Create a new empty folder there and export the path to a variables.

    mkdir ~/streams
    export STREAMS=$(cd ~streams; pwd)

### Create a configuration file to hold secrets
  
    cd $STREAMS
    touch reference.conf
  
To get started, put the following into reference.conf

    twitter {
        oauth {
            consumerKey = ""
            consumerSecret = ""
            accessToken = ""
            accessTokenSecret = ""
        }
    }

Visit developer.twitter.com to obtain the above fields and put them your reference.conf


