# Rasp-Control
Nodejs based small remote control

## Configure Extra Button
There is first button that serves like a return button. It can be set via the Get Parameters:
* returnUrl={url}
* returnName={string}

I use it like this to get back to the main dashboard of my Raspery (in Kiosk mode), e.g.
```
http://localhost:2222/?returnUrl=https://dashboard.page&returnName=Dashboard#
```


## run script on startup

[See Editing rc.local](https://raspberrypi-guide.github.io/programming/run-script-on-boot)

I used an extra startup file:

```
#!/bin/bash
cd /home/fil/code/Rasp-Control
bash -c 'sudo /usr/bin/node /home/fil/code/Rasp-Control/index.js >> /home/fil/code/Rasp-Control/index.log 2>&1' &
```

### Restart your script

```
# Search for the root process with
ps -aux | grep "Rasp-Control/index.js"

# There are serveral lines, it's this one
root       446  0.3  3.9 160732 36864 ?        Sl   09:44   0:03 /usr/bin/node /home/fil/code/Rasp-Control/index.js

# kill the process
sudo kill 446

# restart | See run script on startup
```
