# facebook-live-video
Stream a website with phantomjs to Facebook Live via ffmpeg (video) and collect Facebook reactions

![](https://www.dropbox.com/s/9dyjhg0vvbvjnse/Screenshot%202016-11-15%2022.11.59.png?dl=1)

### Resources

Overview:
https://developers.facebook.com/docs/videos/live-video
API Doc:
https://developers.facebook.com/docs/graph-api/reference/live-video/#Overview

# Installation

I installed everything on Ubuntu 16.04, for other versions check docs how to install.

## FFmpeg

```
sudo apt-get update
sudo apt-get install ffmpeg
``` 

## NodeJS

Install latest NodeJS on your server - you can do it ;) 

## phantomjs

I used the self-contained binary. Check http://phantomjs.org/download.html

```
sudo apt-get update
sudo apt-get install build-essential g++ flex bison gperf ruby perl \
  libsqlite3-dev libfontconfig1-dev libicu-dev libfreetype6 libssl-dev \
  libpng-dev libjpeg-dev python libx11-dev libxext-dev
wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2
tar -xf phantomjs-2.1.1-linux-x86_64.tar.bz2
rm -rf phantomjs-2.1.1-linux-x86_64.tar.bz2
sudo cp phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/bin/
rm -R phantomjs-2.1.1-linux-x86_64
```

# Usage

1. Create Facebook App (if you dont already have one) [>> FB App](https://developers.facebook.com/apps)
1. Get Facebook User Access Token with this app and your user [>> Explorer](https://developers.facebook.com/tools/explorer/)
   Important: User needs `publish_actions` permission
1. Go to your cli and type in:
```
npm start [accessToken]
```

It creates a Live Video (via FB API) and streams the index.html inside the /website folder.
Modify this files for your needs. ;)

The video is set to privacy:SELF, only you can see it.

Check your Facebook wall. ;)

# Configuration

Go to `src/index.js` and checkout the function `start()` there is another function call:
```
fb.startLiveVideo({
    accessToken,
    title: 'First test video - ' + new Date(),
    // privacy: "{'value':'FRIENDS'}"
})
```
modify the options object to configure your stream
see: https://developers.facebook.com/docs/graph-api/reference/live-video/#Overview
for possible parameters.

You can find `privacy` settings here: (search for privacy)
https://developers.facebook.com/docs/graph-api/reference/v2.8/post

---

Modify the files in `/website` how you like. You can also stream another website by changing the `url` in the `index.js` file
# Debug

If you have problems with your installation, check the stream.log:
``` 
tail -f stream.log
```

If you just want to fake increase the reaction counter use :
```
npm start [accessToken] [debug]
=> npm start [accessToken] true
```
It will increase the numbers every 2 sec by a random number.

# Happy hacking ;)