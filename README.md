# node-hikvision-api

[![GPL-3.0](https://img.shields.io/badge/license-GPL-blue.svg)]()
[![npm](https://img.shields.io/npm/v/npm.svg)]()
[![node](https://img.shields.io/node/v/gh-badges.svg)]()

NodeJS Module for communication with Hikvision IP Cameras.

## Status: Work in Progress

## Example:
```javascript
#!/usr/bin/nodejs
var     ipcamera	= require('node-hikvision-api');

// Options:
var options = {
	host	: '192.168.1.100',
	port 	: '80',
	user 	: 'admin',
	pass 	: 'password123',
	log 	: false,
};

var hikvision 	= new ipcamera.hikvision(options);

// Switch to Day Profile
hikvision.nightProfile()

// PTZ Go to preset 10
hikvision.ptzPreset(10)

// Monitor Camera Alarms
hikvision.on('alarm', function(code,action,index) {
	if (code === 'VideoMotion'   && action === 'Start')  console.log(getDateTime() + ' Channel ' + index + ': Video Motion Detected')
	if (code === 'VideoMotion'   && action === 'Stop')   console.log(getDateTime() + ' Channel ' + index + ': Video Motion Ended')
	if (code === 'LineDetection' && action === 'Start')  console.log(getDateTime() + ' Channel ' + index + ': Line Cross Detected')
	if (code === 'LineDetection' && action === 'Stop')   console.log(getDateTime() + ' Channel ' + index + ': Line Cross Ended')
	if (code === 'AlarmLocal'    && action === 'Start')  console.log(getDateTime() + ' Channel ' + index + ': Local Alarm Triggered: ' + index)
	if (code === 'AlarmLocal'    && action === 'Stop')   console.log(getDateTime() + ' Channel ' + index + ': Local Alarm Ended: ' + index)
	if (code === 'VideoLoss'     && action === 'Start')  console.log(getDateTime() + ' Channel ' + index + ': Video Lost!')
	if (code === 'VideoLoss'     && action === 'Stop')   console.log(getDateTime() + ' Channel ' + index + ': Video Found!')
	if (code === 'VideoBlind'    && action === 'Start')  console.log(getDateTime() + ' Channel ' + index + ': Video Blind!')
	if (code === 'VideoBlind'    && action === 'Stop')   console.log(getDateTime() + ' Channel ' + index + ': Video Unblind!')
});

function getDateTime() {
	var date = new Date();
	var hour = date.getHours();
	hour = (hour < 10 ? "0" : "") + hour;
	var min  = date.getMinutes();
	min = (min < 10 ? "0" : "") + min;
	var sec  = date.getSeconds();
	sec = (sec < 10 ? "0" : "") + sec;
	var year = date.getFullYear();
	var month = date.getMonth() + 1;
	month = (month < 10 ? "0" : "") + month;
	var day  = date.getDate();
	day = (day < 10 ? "0" : "") + day;
	return year + "-" + month + "-" + day + " " + hour + ":" + min + ":" + sec;
}
```

## Functions:
```javascript
// Switch Camera to Night Profile
hikvision.dayProfile()

// Switch Camera to Night Profile
hikvision.nightProfile()

// Issue hikvision RAW PTZ Command (See API Manual in GitHub Wiki)
hikvision.ptzCommand(cmd,arg1,arg2,arg3,arg4)

// Go To Preset
hikvision.ptzPreset(int)

// PTZ Zoom, input level: positive = zoom in / negative = zoom out
hikvision.ptzZoom(float)

// PTZ Move
// Directions = Up/Down/Left/Right/LeftUp/RightUp/LeftDown/RightDown
// Actions = start/stop
// Speed = 1-8
hikvision.ptzMove(direction,action,speed)

// Request current PTZ Status
hikvision.ptzStatus()

// Callback for any Alarm (Motion Detection/Video Loss & Blank/Alarm Inputs)
hikvision.on('alarm', function(code,action,index){  });

// Callback for PTZ Status
hikvision.on('ptzStatus', function(data){  });

// Callback on connect
hikvision.on('connect', function(){  });

// Callback on error
hikvision.on('error', function(error){  });

```

## Options
* host - hostname of your hikvision camera
* port - port for your hikvision camera (80 by default)
* user - username for camera
* pass - password for camera
* log - boolean to show detailed logs, defaults to false.

## More Info:
* Support & Discussion:

## About:
By: Ryan Hunt
