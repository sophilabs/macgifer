# MacGifer

[![No Maintenance Intended](http://unmaintained.tech/badge.svg)](http://unmaintained.tech/)

In a divided world, streaming formats are a matter of inclusion. GIF was introduced by CompuServe in 1987, they didn't know how powerful it was going to be. 26 years later, using NodeJS together with Redis, WebRTC, websockets, webworkers and HTML5, MacGifer introduces GIF-based streaming, making it possible for Internet Explorer 6.0 to be part of society once again.

## Requirements
```sh
# Redis
sudo add-apt-repository ppa:chris-lea/redis-server
sudo apt-get update
sudo apt-get install redis-server
```

## Deploying

```sh
# using the included script
./deploy nko
```

## How does it work?
```
        Browser                      Node.js                  Browser/phone
     (broadcaster)                    server                mplayer/microwave
           .                            .                       (watcher)
           |                            |                           .
           |--.                         |                           |
           |  | Get webcam frame        |<--------------------------|
           |  | (WebRTC)                |--.     HTTP Request       |
           |<-`                         |  |                        |
           |--.                         |  | Encode GIF header      |
           |  | Draw on                 |  | (GIFEncoder)           |
           |  | HTML5 canvas            |  |                        |
           |<-`                         |<-`                        |
           |--.                         |-------------------------->|
           |  | Apply                   |       Write header        |
           |  | extensions              |        to response        |
           |<-`                         |                           |
           |--.                         |                           |
           |  | Encode frame            |                           |
           |  | (GIFEncoder)            |                           |
           |<-`                         |                           |
           |--------------------------->|--.                        |
           |         Send frame         |  | Publish to             |
           |        (websockets)        |  | Redis channel          |
           |                            |<-`                        |
           |                            |--.                        |
           |                            |  | Read from              |
           |                            |  | Redis channel          |
           |                            |<-`                        |
           |                            |-------------------------->|
           |                            |       Write frame         |
           |                            |       to response         |
           |                            |                           |
           `                            `                           `
```

## Authors
* [Eduardo Veiga](https://github.com/cinemascop89)
* [Pablo Ricco](http://github.com/pricco)
* [Sebastian Nogara](http://github.com/snogaraleal)

## Credits and Thanks
* The authors of GIFEncoder.js, LZWEncoder.js and NeuQuant.js
* This project was created for the [Node.js Knockout](nodeknockout.com/)

## License
MacGifer is Copyright (c) 2017 sophilabs, inc. It is free software, and may be
redistributed under the terms specified in the [license](/LICENSE) file.

## About

[![sophilabs.co](https://s3.amazonaws.com/sophilabs-assets/logo/logo_300x66.gif)](https://sophilabs.co)

MacGifer is maintained and funded by sophilabs, inc. The names and logos for
sophilabs are trademarks of sophilabs, inc.

