## Create a local folder to configure streams

Pick a place on your file system that's easy to remember and reference with an absolution path.

Create a new empty folder there and export the path to a variables.

    mkdir ~/streams
    export STREAMS=$(cd ~streams; pwd)

Next, create a configuration file to hold secrets for your streams to use.
  
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

Visit developer.twitter.com and create an application to obtain the above fields.

The consumerKey and consumerSecret are application-wide.

The accessToken and accessTokenSecret are per-user.  They can be obtained by navigating to:

    https://api.twitter.com/oauth/authenticate?oauth_token=UIJ0AUxCJatpKDUyFt0OTSEP4asZgqxRwUCT0AMSwc&oauth_callback=http%3A%2F%2Foauth.streamstutorial.w2odata.com%3A8080%2Fsocialauthdemo%2FsocialAuthSuccessAction.do


