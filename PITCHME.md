Hello smugglers
+++
What we are going to do in this workshop?
- a tiny version of the internet
- an embodied website
- a website smuggling device 

has any of you ever made a website?
+++
what do you know about the internet?
+++
### ARPANET
December 1969

![dec 1969](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_500/v1515739389/ws-smugglers/arpanet_dec_1969.jpg)

source: http://som.csudh.edu/fac/lpress/history/arpamaps/
+++
### ARPANET
June 1970

![june 1970](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_500/v1515739392/ws-smugglers/arpanet_june_1970.jpg)
+++
## ARPANET
June 1974

![june 1974](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_500/v1515739398/ws-smugglers/arpanet_june_1974.jpg)
+++
## ARPANET
March 1977

![March 1977](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_500/v1515739414/ws-smugglers/arpanet_mar_1977.jpg)
+++
What happens when you go to `google.com`?
(like really really)
---
## The ESP8266 chip

![ESP8266](http://res.cloudinary.com/zilogtastic/image/upload/v1515739815/ws-smugglers/esp8266-wifi-ic.png)
+++
## The Wemos D1 mini pro
![wemos d1](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_480/v1515739814/ws-smugglers/wemos_d1_mini_pro_v1.0.0_1.jpg)
+++
## Programming for the ESP8266
+++
### APIS and languages
Arduino (C++), Lua, micropython (python 3), ESP SDK (C)
+++
### micropython
we will be using micropython
[micropython.org](https://micropython.org/)
---
### Getting our workstation ready
Install wemos drivers (https://wiki.wemos.cc/products:d1:d1_mini_pro)
+++
### getting our workstation ready
We will be needing some command line tools to flash our firmware. `esptool` is a small python utility that
allows us to upload binaries to our ESP board.

```
$ pip install esptool
```
Once it installs successfully run it and read the help text
+++
### What is flashing?
+++
### getting our workstation ready
flashing the firmware: loading micropython into the Wemos D1 mini Pro

You will need to download a binary file from the micropython downloads area: http://micropython.org/download/ named `esp8266-20171101-v1.9.3.bin`. This file contains a new firmware for the ESP8266 chipset that implements the core of python.
+++
### getting our workstation ready
You will need a terminal emulator for the next few steps, Linux and OSX come with one: `screen`. 

Windows lacks a terminal emulation program so you need a third party program like PuTTY. You can download it from (PuTTY's homepage: https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html.
---
### Working with micropython
interacting with the board through micropython code using the serial REPL

```
$ screen /dev/tty.SLAB_USBtoUART 115200
```

*REPL stands for Read Evaluate Print Loop* it is an interactive programming environment, many languages offer this way of interfacing with their runtime.
+++
##### Note for Unix people

if you like scaperooms, try `screen`

The `screen` fairly awkward to use and has a steep learning curve. For now we just need to know how to open a session using the command above to quit you can use <kbd>ctrl</kbd> + <kbd>a</kbd> and then <kbd>ctrl</kbd> + <kbd>k</kbd>, then it will ask you if you want to kill the window. You can use this moment to ponder about the meaning of *kill* in this context, or you can just press <kbd>y</kbd> to exit.
+++
## Working with micropython: The WebREPL

Let's use the serial interface to access the board's REPL and enabled the WebREPL feature so that we can use our browser to type in our code instead of the terminal.

```
import webrepl_setup
```
+++
## Working with micropython
listing files in the board's file system, what do you see?

can Arduino hold files like this? why not?
+++ 
## Working with micropython
things you can try to do: get board diagnostics, get the devices MAC address, install packages with upip, run your own python game?
+++
## Working with micropython: ESPlorer
A bit more user friendly and versatile.

[https://esp8266.ru/esplorer/](https://esp8266.ru/esplorer/)
+++
next, let's look at wifi capabilities
---
## Wifi
perhaps the ESP's most appealling feature is the wifi support. We can use it from micropython and configure our board to function in two different modes "base station" and "access point".
+++
## Wifi & micropython
connecting to wifi as a client

```
import network

station = network.WLAN(network.STA_IF)
station.active(True)
station.connect("smugglers", "smugglers")
station.isconnected()
```
+++
## Wifi & micropython
what else is around us? scanning wifi nodes

```
station.scan()
```
+++
## Wifi & micropython
making a simple access point (AP)

```
import network

ap = network.WLAN(network.AP_IF)
ap.config(essid="MONKEY_ISLAND", authmode=network.AUTH_OPEN, channel=11)
```

try and connect your workstation to that access point now: what's your new IP?, who is your gateway?
+++
## Wifi & micropython
making a simple access point (AP)

```
ap.ifconfig()
```

Will show us our device's IP, netmask, gateway IP and DNS address.
+++
now that we know a little bit more about networking, let's build our very own ARPANET
---
## Our very own ARPANET
+++
## building a network
we are going to need a router... what's a router?
+++
## building a network
adding your smuggler-board to the routers configuration and giving each a domain

please give me your boards MAC address, IP address and the domain name you wish to give it
+++
## building a network
try to ping your board using the new-flanged domain name
+++
now we have all these networking little devices, but they are not yet running any services, to make our network be something interesting we are going to need to run services on it, like for example a DWW - darknet wide web.
---
## building a tiny server
what is a server? how does it look like? and what does it do?
+++
## what is a server?

![U1 rack unit](http://res.cloudinary.com/zilogtastic/image/upload/v1515742877/ws-smugglers/U1-server.png)
+++
![rack](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_500/v1515742880/ws-smugglers/server-rack.jpg)
+++
![network operator at DC](http://res.cloudinary.com/zilogtastic/image/upload/v1515742878/ws-smugglers/geek-at-dc.jpg)
+++
<iframe src="https://player.vimeo.com/video/95044197?color=ffffff&byline=0&portrait=0" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

*Timo Arnall, 2014*

Film: 6 min 40 sec, digital 4K, 25fps, stereo.
Installation: Digital projection, 3 x 16:10 screens, each 4.85m x 2.8m.
Medium: Digital photography, photogrammetry and 3D animation.
+++
can one webserver have more than one website?
+++
## building a tiny webserver
- opening a socket in micropython
- binding to socket on port 80
- what is 0.0.0.0?
- listening forever
+++
## building a tiny webserver 
HTTP request/response [RFC2616](https://www.w3.org/Protocols/rfc2616/rfc2616.html)
+++
## building a tiny webserver 
what do web requests and responses look like?
(open your browser's developer tools)
+++
## building a tiny webserver 
- what is 404?
- what is 200?

See: [https://httpstat.us/](https://httpstat.us/)
+++
## building a tiny webserver 
sending back a 200 success page with a message in the body
+++
## building a tiny webserver
understanding the request: print the request and observe it carefully. What is it? What information does it 'leak'?
+++
## building a tiny webserver
- what's in a URL? 
- what is it? 
- what does the URL correspond to in the server?
+++
## building a tiny webserver
exercise: building your own parse/router
+++
## building a tiny webserver
serving the first webpage page ever
+++
now we know how to build a small darknet all of our own, were we own the infrastructure and wrote the code for its services! congrats!
+++
on the internet, however, the story is a fair bit more complex
---
# Internet censorship case studies
+++
## Turkey: Gezi park protests 2013
+++
Highest priority for Erdogan was to block access to social media sites, specially Twitter.
+++
Used easy to circumvent DNS blockades
+++
![google DNS graffitti](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_500/v1515745428/ws-smugglers/beyond_the_hashtag_gezi_dns_graffitti.jpg)
+++
### #direntwitter
![#direntwitter](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_500/v1510850656/cat_referendum/Alternative_DNS.jpg)

+++
## North Korea and the Internet of 28 websites

http://www.telegraph.co.uk/technology/2016/09/21/north-koreas-internet-revealed-to-have-just-28-websites/

+++

## Catalonia's referendum
##### 1 Oct 2017

+++
![web censurada del referendum](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_600/v1510847839/cat_referendum/Screen_Shot_2017-11-16_at_15.59.43.png)

+++

![the referendums web](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_600/v1510847838/cat_referendum/Screen_Shot_2017-11-16_at_15.48.07.png)

+++

![github repo with mirror](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_600/v1510851285/cat_referendum/Screen_Shot_2017-11-16_at_17.54.19.png)

+++

![servidores en cloudflare](http://res.cloudinary.com/zilogtastic/image/upload/v1510847838/cat_referendum/Screen_Shot_2017-11-16_at_15.46.09.png)

+++

The _OnVotar_ census website asked for 3 pieces of information:
- Your national identity number (similar to the Dutch BSN Burgerserviesnummer)
- Your date of birth
- Your postal code

This information is highly sensitive given the context. The surveillance and retaliatory powers of the Spanish state made it possible to send every voter to court.

+++

How do you build an electronic census online, on the open Internet, knowing that you must protect voter's private information and knowing that the Spanish state will do everything they can to retaliate?

+++

Hmmm... tricky! The strategies for the digital census the day of the Catalonian referendum is a great study case on countermeasures for digital censorship.

+++

When you click on the button labelled "Search a polling station" the site makes a `GET` request, with the following content:

```
Request URL:https://onvotar.garantiespelreferendum.com/db/c3/a1.db
Request Method:GET
Status Code:200
Remote Address:104.18.36.145:443
Referrer Policy:no-referrer-when-downgrade
Origin:null
User-Agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36
```

The form data *is not sent* to the server! This is unsual.

+++

Fetching that file in the request reveals the following:

```
1febc7fc1f60ae314b424303ea516a290f305a36c0bab4f3dbc98d810f2ee162e59878057968a22bbaa69a9dc066414f1506a8d10dfa1d73130b3ee2f4bf9037c7ab8642528c9b0c5c157b4ea0dd9bbb1815c5b2bd4519852e59c4bac040599db36127f0f52530b7f45455f9d4fa55798a9918a65391c49a0181c677da360346da22e7b0c33b05bfcbb55a4ee75820fe1f9fbdd532b40ccac4c6ba85d610679b66bad2a43fbb2a418eec58c4772a42113b3fa25052c2435c5c4a5ffe8bcaf2896d220eaa4c446f19c62b26ccefd3
e4d353eeb673c351f84276fb8c159381ff641775b9e0a17925245f39bedd33661212588b3ca926ee31a49859055f901382279a24c291076660b3e80e65de8ec66e948bc64b5120ae09dd56f955302e1323ef8afdd29143269f2b7c3a8e6c02ebc70d0c9d949092ca19246d5cba3b0c69c314bf7d7a4222326fd7b78c8768e029e4e5ef1175ed5dd457ce3fc88840f9ce941eeb2bd28521ac5eb8be1be9faf1b40ee3f2f81683be3c3a93f1b806aaa5ff7761b873a725ff470a67983d3d827bbbdfcb228c4ec505b4347945c39ab9
2fd03efea47e19d24331a4b6b0ffa9988efda433d5ad5a31c10d2b0b849ee2013e7be6ccb75336147a600c7f542b702289d843d683156797e32e360a5e96f499c0350ba3de76fbe91694463381b9ff1fbf4820ab215b03da5cf604b5523530c9d21ca7f84e150e8ad3cd08d06f05c6cf81c9e87ee49ee60d709496a1ca35a5a742992cb9736bcbf64295a0103b44c3cb7ea0e923a0a1bd3540abb6a0ec78bf56f94967b2ec92ab8000bec75d4dddcb12f0651d062693c068714cd449e45692eb3ef3821db6c1302ff5e57d572d1d
...
```
This is some kind of encoded database. Not entirely clear what it is. Things are getting weird now.

+++

The `index.html` file reveals what your browser does next:

```
function calcula() {
  document.querySelector("#stepLoad").style.display="inline"
  var dni = document.querySelector("#dni").value
  dni = dni.replace(/ /g,'').replace(/-/g,'').replace(/\./g,'');
  var dn_dia = document.querySelector("#dn_dia").value
  var dn_mes = document.querySelector("#dn_mes").value
  var dn_any = document.querySelector("#dn_any").value
  var cp = document.querySelector("#cp").value
  if (dn_dia.length == 1)
     dn_dia = "0"+ dn_dia
  if (dn_mes.length == 1)
     dn_mes = "0"+ dn_mes
  if (dn_any.length == 2)
     dn_any = "19" + dn_any
  onvoto.calcular(dni.slice(-6),dn_any+dn_mes+dn_dia,cp, function(i) {
    document.querySelector("#stepLoad").style.display="none"
    if (( typeof i === 'string' ) && ( i == 'not-found' ))  {
        document.querySelector("#response").innerHTML = "No s'ha trobat cap registre corresponent a les dades introduïdes."
    } else {
       document.querySelector("#stepOne").style.display="none";
       document.querySelector("#response").innerHTML = i[0] + "\n" + i[1] + "\n" + i[2] + "\n\n"
                                                     + "Districte:" + i[3] + "\n" + "Secció:" + i[4] + "\n"
                                                     + 'Mesa: ' + i[5];
    }
   })
}
</script>
```
This code seems to try to use your personal data to create some kind of key and that key is used again later in the code [...]

+++

```
var calcular = function (d, dn, cp, cb){
    ...
    var key = dni + data_naixement + codi_postal;
    var firstSha256 = hash(bucleHash(key,BUCLE));
    var secondSha256 = hash(firstSha256);
    var dir = secondSha256.substring(0,DIRSHA);
    var file = secondSha256.substring(DIRSHA,DIRSHA+FILESHA);
    var url = window.location.href.replace('/index.html','/');
    ...
    url += '../db/' +dir + "/" + file + FILEEXTENSION;

    request( url, function (error, response, body) {
    ...
```
This calculates a _shard_ number. This means that they split the database into multiple tiny databases called _shards_.

+++
![](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_500/v1515744811/ws-smugglers/cat_db-sharding.png)
source: matthias @ 34c3
+++

The number of shards indicates that there are about 65000 of them, and each shard contains the personal data of about 70 Catalonians elligible to vote. 70 times 65000 is about 4.5 million, which seems about correct. 4.5 million people in Catalonia are elligible to 
vote.

+++

Each _shard_ is encrypted, using the voter's own personal data hashed 17 times. It would take a very fast desktop computer about 31.000 years to _brute force_ that hash. A state like Spain can do it in much less, *but the expense is considerable*. If the police did break it (as they claimed on the press days later without any evidence), it probably cost the Spanish tax payer a lot of money to break that encryption.

+++

13 September 2017, a judge gave national telecoms 24h to block the 10 known websites hosting the website of the Catalonian Referendum

+++

![github repo of whatsapp bot](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_600/v1510852160/cat_referendum/Screen_Shot_2017-11-16_at_18.08.46.png)

+++

Website was Grade A according to SSLlabs, this is the highest ranking and certifies a proper implementation of HTTPS.

+++

![estonia](http://res.cloudinary.com/zilogtastic/image/upload/v1510848703/cat_referendum/screencapture-politica-elpais-politica-2017-10-13-actualidad-1507916636_098849-html-1510848636384.png)

+++

![telegram bot](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_600/v1510847838/cat_referendum/Screen_Shot_2017-11-16_at_15.57.06.png)

+++

![papeleta en google drive](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_600/v1510847838/cat_referendum/Screen_Shot_2017-11-16_at_15.48.44.png)

+++

![encouraging people to send the apps APK package via whatsapp](http://res.cloudinary.com/zilogtastic/image/upload/c_scale,h_600/v1510847839/cat_referendum/Screen_Shot_2017-11-16_at_15.54.15.png)

+++

With a website, several hundred domains, servers in Spain and abroad, a Whatsapp bot, a Telegram bot and a self-dispatching census app as APK package. The different digital strategies adopted by Catalonians for the independence referendum conform the most "all out" and overt digital campaign I am aware of.

+++

It is worth noting that there was not a single mind behind this "digital straetgy", meaning that it was not centrally coordinated by the Catalonian Govern, but rather different citizens with different areas of expertise contributed with their own tactics.

+++

## Telecoms
#### How telecoms implemented the order to censor the referendum

+++

## DNS blokade 

This was what most telecoms did: Orange and other telecoms that use their network (Jazztel, SomConnexió. As well as other telecoms with their own network Euskaltel, Vodafone.

+++

### Remember #direntwitter

The DNS blokades were a common censorship measure during the Gezi protests, and have become commonplace in Turkey since.
+++

## Movistar
#### Telefonica's mobile network.

They used a primitive form of DPI (deep packet inspection).
- For regular HTTP connections they used hostname and IP blacklists.
- For HTTP*S* connections they look up the field SNI (unencrypted hostname in the TLS message) and the IPs.

![movistar DPI](http://res.cloudinary.com/zilogtastic/image/upload/v1510850566/cat_referendum/movistar-wireshark-mitm.png)

+++

### Parlem telefonia
They announced that no content would be censored on their network

+++

---
## design challenge: becoming a website smuggler
choose any of the countries that appear in this censorship report made by *Freedom House* in 2016
[https://freedomhouse.org/report/freedom-net/freedom-net-2016
](https://freedomhouse.org/report/freedom-net/freedom-net-2016)

and research deeper into how the internet is censored in those countries, what websites or protocols? who is censored and why? what are the motivations behind the censorship?

Think up of a way to smuggle a website into the country of your choice? What website would you take with you? and how would you smuggle into the country using this simple setup we made today?

**!!! website may not exceed 3Mb in size, all inclusive !!!**

+++
## kickstart your research
Here are some sites that you can use to begin your research:

network monitoring organizations:
- https://ooni.torproject.org/
- https://atlas.ripe.net/

reports, articles and readers:
- https://www.eff.org/free-speech-weak-link
- https://freedomhouse.org/report/freedom-net/freedom-net-2016
- http://projects.interactiefarnhem.nl/behind-the-net/reader/
- https://opennet.net/
- https://onlinecensorship.org/resources/further-readings
- https://citizenlab.ca/
- https://medium.com/on-archivy/the-web-as-a-preservation-medium-3d697328b3b8
---
Thank you and see you tomorrow!
