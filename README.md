# simcorder demo - RTP recording

In this example, a browser's webcam media is transmitted to [mediasoup](https://mediasoup.org/) using WebRTC ([WebRtcTransport](https://mediasoup.org/documentation/v3/mediasoup/api/#WebRtcTransport)); it is then served as a plain RTP stream ([PlainTransport](https://mediasoup.org/documentation/v3/mediasoup/api/#PlainTransport)) to be received and recorded by an external process(GStreamer).

**The media is not re-encoded at any moment**. This is an important detail, because you want recording to take as little resources as possible. For that, the and GStreamer commands are carefully written to make sure that the media packets are received via RTP and get stored as-is to the output recording file.



## Setup

mediasoup applications are written for [Node.js](https://nodejs.org/), so you need to have it installed. Follow the [installation instructions](https://github.com/nodesource/distributions/blob/master/README.md) provided by NodeSource to install Node.js from an official repository; or just grab it from the official [downloads page](https://nodejs.org/en/download/).



### Installing GStreamer

In Debian/Ubuntu systems, run the following command in a terminal:

```sh
sudo apt-get update && sudo apt-get install --yes \
    gstreamer1.0-plugins-{good,bad,ugly} \
    gstreamer1.0-{libav,tools}
```



### Safely run Node.js on port 80 and 443

You will be using port 80 and 443 to run your app, which typically can only be accessed by the root user. (You will able to run your app using a custom URL such as http://mysite.com - but you will not have to specify a port.). Run the following command in a terminal: (subtitute `path/to/node` with your path to *node* executeable. Usually `/usr/bin/node`)

```sh
sudo apt-get install --yes libcap2-bin
sudo setcap cap_net_bind_service=+ep /path/to/node
```



## Run

Run these commands:

```sh
npm install

npm start
```

