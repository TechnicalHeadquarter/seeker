
<p align="center">
<img src="https://img.shields.io/badge/Python-3-brightgreen.svg?style=plastic">
<img src="https://img.shields.io/badge/Docker-✔-blue.svg?style=plastic">
</p>

<p align="center">
  <a href="https://t.me/TechnicalHeadquarter"><b>Telegram</b></a>
  <span> - </span>
</p>

<p align="center">
  <br>
  <b>Available in</b>
  <br>
  <img src="https://i.imgur.com/1wJVDV5.png">
</p>

Concept behind Seeker is simple, just like we host phishing pages to get credentials why not host a fake page that requests your location like many popular location based websites. More on <a href="https://youtube.com/TechnicalHeadquarter"> My Youtube channel </a>.Seeker Hosts a fake website on **In Built PHP Server** and uses **Serveo** to generate a link which we will forward to the target, website asks for Location Permission and if the target allows it, we can get :

* Longitude
* Latitude
* Accuracy
* Altitude - Not always available
* Direction - Only available if user is moving
* Speed - Only available if user is moving

Along with Location Information we also get **Device Information** without any permissions :

* Operating System
* Platform
* Number of CPU Cores
* Amount of RAM - Approximate Results
* Screen Resolution
* GPU information
* Browser Name and Version
* Public IP Address
* IP Address Reconnaissance

**This tool is a Proof of Concept and is for Educational Purposes Only, Seeker shows what data a malicious website can gather about you and your devices and why you should not click on random links and allow critical permissions such as Location etc.**

## How is this Different from IP GeoLocation

* Other tools and services offer IP Geolocation which is NOT accurate at all and does not give location of the target instead it is the approximate location of the ISP.

* Seeker uses HTML API and gets Location Permission and then grabs Longitude and Latitude using GPS Hardware which is present in the device, so Seeker works best with Smartphones, if the GPS Hardware is not present, such as on a Laptop, Seeker fallbacks to IP Geolocation or it will look for Cached Coordinates.  

* Generally if a user accepts location permsission, Accuracy of the information recieved is **accurate to approximately 30 meters**, Accuracy Depends on the Device.

**Note** : On iPhone due to some reason location accuracy is approximately 65 meters.

## Templates

You can choose a template which will be used by seeker from these : 

* NearYou
* Google Drive 
* WhatsApp 
* Telegram

## Tested On :

* Kali Linux
* BlackArch Linux
* Ubuntu
* Kali Nethunter
* Termux
* Parrot OS

## Installation

### Kali Linux / Ubuntu / Parrot OS

```bash
git clone https://github.com/TechnicalHeadquarter/seeker.git
cd seeker/
chmod 777 install.sh
./install.sh
```

### BlackArch Linux

```bash
pacman -S seeker
```


### Termux

```bash
git clone https://github.com/TechnicalHeadquarter/seeker.git
cd seeker/
chmod 777 termux_install.sh
./termux_install.sh
```

## Usage

```bash
python3 seeker.py -h

usage: seeker.py [-h] [-s SUBDOMAIN]

optional arguments:
  -h, --help                              show this help message and exit
  -s SUBDOMAIN, --subdomain Subdomain 	  Provide Subdomain for Serveo URL ( Optional )
  -k KML, --kml KML                       Provide KML Filename ( Optional )
  -t TUNNEL, --tunnel TUNNEL              Specify Tunnel Mode [manual]

# Example

# SERVEO 
########
python3 seeker.py

# NGROK ETC.
############

# In First Terminal Start seeker in Manual mode like this
python3 seeker.py -t manual

# In Second Terminal Start Ngrok or any other tunnel service on port 8080
./ngrok http 8080

#-----------------------------------#

# Subdomain
########### 
python3 seeker.py --subdomain google
python3 seeker.py --tunnel manual --subdomain zomato

#-----------------------------------#

## Known Problems

* Services like Serveo and Ngrok are banned in some countries such as Russia etc., so if it's banned in your country you may not get a URL, if not then first READ CLOSED ISSUES, if your problem is not listed, create a new issue.
..........................................
You can use any website you want, just keep the javascript and php intact, don't change any variables, if you really want to change variables then carefully analyse both javascript and php and you will be able to use your own variables, this is a great idea i will give it a try, it will be something like SET

Websites templates are under /seeker/template

/opt/seeker/template# ls
nearyou sample.kml

copy nearyou as twitter (new template name as you want)

/opt/seeker/template# cp -r nearyou/ /opt/seeker/template/twitter
/opt/seeker/template# ls
nearyou sample.kml twitter

navigate inside the twitter folder

/opt/seeker/template# cd twitter/
/opt/seeker/template/twitter# ls
css index.html js php

and edit the index.html as you want
/opt/seeker/template/twitter# geany index.html

finally edit the seeker.py script

#result = 'template/nearyou/php/result.txt'
#info = 'template/nearyou/php/info.txt'
#site = 'nearyou'

result = 'template/twitter/php/result.txt'
info = 'template/twitter/php/info.txt'
site = 'twitter'

#php_rqst = requests.get('http://127.0.0.1:8080/nearyou/index.html')
php_rqst = requests.get('http://127.0.0.1:8080/twitter/index.html'

python3 seeker.py -t default -s twitter

or

python3 seeker.py -t default	
