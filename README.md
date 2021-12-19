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


## run script on startup via rc.local

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

## run script on startup via systemd
[See | Running Your Node.js App With Systemd - Part 1](https://nodesource.com/blog/running-your-node-js-app-with-systemd-part-1/)
```
sudo nano /lib/systemd/system/raspcontrol.service 
```
Content
```
[Unit]
Description=Rasp Control
Documentation=https://github.com/thespielplatz/Rasp-Control
After=network.target

[Service]
Environment=NODE_PORT=80
Type=simple
User=root
WorkingDirectory=/home/fil/code/Rasp-Control
ExecStart=/usr/bin/node index.js
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
then
```
# Start it
sudo systemctl daemon-reload
sudo systemctl start raspcontrol

# Read log files
journalctl -u raspcontrol.service
journalctl -u raspcontrol.service --since today

# Enable for Startup
sudo systemctl enable raspcontrol
```

For more info about logging [see](https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs)
