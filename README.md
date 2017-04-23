# raspberry-camera
application for live-streaming camera feed

based on [h264-live-player](https://github.com/131/h264-live-player)

git clone  https://github.com/131/h264-live-player.git
cd h264-live-player-master
node server-rpi.js //you can check which port it uses - last line, this should spawn a raspivid process

in your frontend application make sure to get the http-live-player.js script like so:
<script src="http://78.88.254.231:5000/http-live-player.js"></script>

then as a POC i used this hack ember componenet to get it to work:

JS:
import Ember from 'ember';

export default Ember.Component.extend({
  didRender() {
      setTimeout(() => {
        const canvas = this.$('canvas').get(0);
        var uri = "ws://78.88.254.231:5000";
        var wsavc = new WSAvcPlayer(canvas, "webgl", 1, 35);
        wsavc.connect(uri);
        //expose instance for button callbacks
        window.wsavc = wsavc;
        setTimeout(function() {
          debugger;
          wsavc.playStream()
        }, 2000)
    }, 2000)
  }
});

HBS:
<canvas width="960" height="540"></canvas>
