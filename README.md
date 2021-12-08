# Rasp-Control
Nodejs based small remote control

### run script on startup

[See Editing rc.local](https://raspberrypi-guide.github.io/programming/run-script-on-boot)

I used an extra startup file:

```
#!/bin/bash
cd /home/fil/code/Rasp-Control
bash -c 'sudo /usr/bin/node /home/fil/code/Rasp-Control/index.js >> /home/fil/code/Rasp-Control/index.log 2>&1' &
```
