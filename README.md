# WebRTC Demo

## About

This is a "simple", but complete example of how to utilize WebRTC to do peer to
peer voice and video calling between two or more people.

Original author: @shastox (great at tech; not so great at JS). Rapidly refactored by @jmsherry

### Server Side

This example uses node.js and socket.io to create a "Signaling Server", which
runs on (or near) your web server to manage who should talk to who. The purpose
of the signaling server is to relay information between peers while you are
setting them up to talk directly to each other.

### Client Side

Included is `main.js`, which contains all of the logic to connect to the
signaling server, join a virtual group chat channel, connect with peers, and
stream video and audio to all party members using the raw WebRTC API.

## Running

### Node.js signaling server

You'll need to install `node.js` as well as the `express` and `socket.io` libraries:

```javascript
npm install -g socket.io express
```

Then simply run the signaling server:

```javascript
node signaling-server.js
```

### Web server

You'll also probably want to host `index.html` on a web server somewhere. You'll need to edit `main.js` and change `YOURSERVERNAMEHERE` to be the hostname or IP of the signaling server.

Note: you can also simply open the file locally instead of using a web server,
but at the time of writing this only firefox will let you access the
webcam/microphone from a file hosted off of your local machine.

### Running the sample

Now navigate to wherever you stuck `index.html` and you should be presented with
a dialog asking permission to access your microphone / webcam. Once accepted,
you should see a local stream appear on the page. Now open up the same page in
another browser, on the same computer or another, and watch as the magic of WebRTC takes effect and both images and audio samples mysteriously move from one browser to the other. Repeat with as many browsers as you dare.

**Note:** At the time of writing this, only firefox and chrome support WebRTC,
however both browsers support this on Windows, Linux, Mac, and Android, so lots
of fun can be had pointing everyones' phones, tablets, and laptops at that `index.html` and bogging down your network with audio/video traffic.

## Using things other than node.js, and socket.io

The choice of node.js and socket.io is based purely on my familiarity with them
and the fact that their fairly easy to understand even if you aren't familiar
with them. However, you can use any mechanisms you want for your signaling system, you just need a way to exchange ICE candidates and session descriptions between
clients.

## Adapter.js

You'll see `index.html` uses `adapter.js`. This "library" just normalizes the
WebRTC API, which will only be necessary while WebRTC is making its way through
the standards process. Once everything is standardized and functions are
de-prefixed in the browsers, this won't be necessary anymore.
