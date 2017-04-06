
Alternatively, (TK: test)

```bash
/usr/bin/pm2 start /home/ec2-user/hello-world-server.js -i 0 --name "node-app"
PM2_HOME=/home/ec2-user/.pm2 /usr/lib/node_modules/pm2/bin/pm2 save
sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemv -u ec2-user --hp /home/ec2-user
PM2_HOME=/home/ec2-user/.pm2 /usr/lib/node_modules/pm2/bin/pm2 save

sudo sed -i '$i /usr/bin/pm2 start /home/ec2-user/hello-world-server.js -i 0 --name \"node-app\"' /etc/rc.local
sudo /etc/rc.local start

sudo sed -i '$i export PATH=$PATH:/.nvm/versions/node/v6.7.0/bin' /home/ec2-user/.bashrc
sudo sed -i '$i . /.nvm/nvm.sh' /etc/rc.d/rc.local
sudo sed -i '$i pm2 start /home/ec2-user/hello-world-server.js -i 0 --name \"node-app\"' /etc/rc.d/rc.local
```
