## /views/index.pug 
```pug
extends layout

block content
  h1 
    img(src='https://cdn.worldvectorlogo.com/logos/nodejs-icon.svg')
    span Node.js - Demoo Web Applucation
  h2 &#x1F4BB; System Info...
  table 
    tr 
      td OS: 
      td #{info.type} &ndash; v#{info.release}
    tr
      td Hostname:
      td #{info.hostname} 
    tr
      td CPUs: 
      td #{info.cpus.length} &times; #{info.cpus[0].model}
    tr
      td Memory: 
      td #{Math.round(info.mem/(1024*1024))} MB
    tr
      td Environment: 
      td #{info.env}     
  if isDocker
    h3 &#x1F4E6; Status: Running in a Docker container! &#x1F604; 
  else
    h3 &#x1F4E6; Status: Not running as a Docker container &#x1F622;
  hr
  h2 Azure &hearts; Open source
```


## /routes/index.js 
```js
var express = require('express');
var router = express.Router();
const os = require('os');
const fs = require('fs');

/* GET home page. */
router.get('/', function (req, res, next) {
  var info = { 
    release: os.release(), 
    type: os.type(), 
    cpus: os.cpus(), 
    hostname: os.hostname(), 
    arch: os.arch(),
    mem: os.totalmem(),
    env: process.env.WEBSITE_SITE_NAME ? process.env.WEBSITE_SITE_NAME.split('-')[0] : 'Local'
  }

  res.render('index', { title: 'Azure Demo App', info: info, isDocker: fs.existsSync('/.dockerenv') });
});

module.exports = router;
```


## /public/stylesheets/style.css 
```css
body {
  padding: 20px;
  font: 18px "Segoe UI Light", "Lucida Grande", Helvetica, Arial, sans-serif;
  color: lightgray;
  background-color: #333333;
}

h1 {
  background-color: #0072C6;
  padding: 20px;
  color: white;
  border-radius: 10px;
}

table {
  background-color: #B8D432;
  color: #000000;
  padding: 10px;
  font-weight: bolder;
  border-radius: 6px;
}
```