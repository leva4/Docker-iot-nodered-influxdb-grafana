FROM nodered/node-red

# Copy package.json to the WORKDIR so npm builds all
# of your added nodes modules for Node-RED
COPY package.json .
RUN npm install --unsafe-perm --no-update-notifier --no-fund --only=production


USER node-red
# copy node-red project files into place
COPY flows.json /data/flows.json
# copy the settings file
COPY settings.js /data/settings.js

# we always want the influxdb plug-in.
RUN npm install node-red-contrib-influxdb
# fix any dependency issues
RUN npm audit fix

# change the startup command to be sure to use our settings.
CMD ["npm", "start", "--", "--userDir", "/data", "--settings", "/data/settings.js"]