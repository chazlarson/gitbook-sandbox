**Can I install Webmin on a server with Cloudbox?**

You can install it and in most cases it won't break any Cloudbox functionality.

Please be aware that whilst Webmin can make some server administration tasks easier or faster it does introduce some risk and complexity. 
Firstly it will run on port 10000 and you shouldn't leave that port open to the public. Use UFW to block that port and/or only give access to your static home IP. 
You should ensure Webmin is updated (it can be set to automatically update) as Webmin has had security issues in the past and could reduce the security of your server.

If you know what you're doing or are willing to accept the extra risk versus convenience of running Webmin please do the following as the root user on Ubuntu 18.04

`sudo nano /etc/apt/sources.list` <br>
Add this line to the bottom of the file <br>
`deb http://download.webmin.com/download/repository sarge contrib` <br>
`wget http://www.webmin.com/jcameron-key.asc` <br>
`sudo apt-key add jcameron-key.asc` <br>
`sudo apt update` <br>
`sudo apt install webmin` <br>
