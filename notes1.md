# ***IPv4 Notes lol***   


best chart for ip_adressing and subnetting
"Binary doubling reference chart"

128_ 64_ 32_ 16_ 8_ 4_ 2_ 1_    
0___ 0__ 0__ 0__ 0_ 0_ 0_ 0_ <- dit is een octet

een octet is een acht-tal binaire eentjes of nullen;

|128|64|32|16|8|4|2|1|| 
|:---|:---|:---|:---|:---|:---|:---|:--|:-
0|0|0|0|0|0|0|1| <- nu is deze octet een decimaal van 1

|128|64|32|16|8|4|2|1|| 
|:---|:---|:---|:---|:---|:---|:---|:--|:-
0|0|0|1|1|1|1|1| <- nu is deze octet een decimaal van 31

|128|64|32|16|8|4|2|1|| 
|:---|:---|:---|:---|:---|:---|:---|:--|:-
0|1|1|1|1|1|1|1| <- nu issie 127 weetjewel

IP adres is 4 x een octet**
dus 32 bits opgebroken in 4 stukjes
192.168.1.5

192 = 11000000

168 = 10101000

1	= 00000001

5	= 00000101

is dus makkelijk uit te rekenen met de chart:    
128_ 64_ 32_ 16_ 8_ 4_ 2_ 1_    
0	 0   0	 0 	 0    
192.168.1.0/24 <- achter de slash is **CIDR notation (Classless Inter Domain Routing)**     
het CIDR getal betekent hoeveel binary digits aan staan in de subnet mask,    
dus hoeveel ééntjes er zijn in de octets   
dus als de subnet mask 255.255.255.0 is is de CIDR notation /24   
want : 11111111.11111111.11111111.00000000 = 24 eentjes.   

je subnet mask laat zien welk gedeelte van de IP deel is van de network ID

wanneer je 255.255.248.0 (CIDR notation 21) over 192.168.40.55 legt krijg je het volgende:

1.|255.|248.|0
-|:-|:-|:-|   
11111111|11111111|11111000|00000000   
192.|168.|40.|55   
11000000|10101000|00101000|00110111   

Network ID

>192.168.40.0/21 <- CIDR notation

>255.255 .248.0	 <- subnet mask   

de subnet mask loopt tot waneer 40 wordt gedefinieerd in het derde octet
dus het Network ID is 192.168.40.0

de rest, de bits die buiten de subnet mask vallen zijn 'host bits'
bijvoorbeeld, wanneer je het IP 192.168.45.55 hebt en de subnet mask is nog steeds 255.255.248.0 
dan heb je:
```
1.       255.     248.     0    
11111111 11111111 11111000 00000000
192.	 168. 	  45.      55
11000000 10101000 00101101 00110111
```
en is je Network ID nog steeds 192.168.40.0 
```
1.       255.     255.     192 
 11111111 11111111 1111111  11 |000000
192.	 168. 	  45.      55  |v|dingen aan deze kant zijn host bits.
 11000000 10101000 00101101 00 |110111
 ```
je 'broadcast' adres is je Network ID + de decimal van wanneer alle binaries aan staan in je host bits    
bijvoorbeeld, in dit geval is het 192.168.45.63     
want van de laatste octet zijn de eerste twee bits deel van de subnetmask, daarna heb je nog     
192.|168.|45.|55||||||||| 
:-|:-|:-|:-|:-|:-|:-|:-|:-|:-|:-|:-|
||||128| 64| 32 |16 |8 |4 |2 |1|||
||||0|0|1|1|1 |1 |1 |1| | |
|	|		|| ||32| + 16|+ 8| + 4|+ 2| + 1 | = 63|

als je iets verstuurt naar de 'broadcast' adres wordt het naar alle adressen in het netwerk gestuurd
er zijn 62 adressen bruikbaar, eentje voor je broadcast. en meestal een voor je router, 
en de rest is vrij om dan anderen aan te verbinden.

255.255.255.0 
/24
is de meest gebruikte subnetmask.
je hebt dan 254 bruikbare adressen.

# Class System

IPv4 heeft verschillende classes

IP classes zijn default classes gebaseerd op het nummer van het eerste octet

class|1st octet range| default mask
--|:-|:-
class A|1 - 126|255.0.0.0
class B|128 - 191|255.255.0.0
class C|192 - 223|255.255.255.0
Loopback|127|  
class D| 224 - 239| Multicasting
Class E| 240 - 255.255.255.254|Experimental

# hoe doe je euh nummer hoeveelheid subnets vinden lol en valid hosts weetje

>Hoeveel subnets?, gewoon '2 tot de macht hoeveelheid subnetbits '   
$hoeveelheid$ $subnets =$ $2 ^ {subnetbits}$   

subnetbits zijn de bits die, naast de mask die gedefinieerd is door de class, zijn opzij gezet voor subnets.

ip:|192.|164.|1.|0.
:-|:-|:-|:-|:-|
mask:|255.|255.|255.|240 (/28)
||11111111|11111111|11111111|11110000|

<img src="a.png" alt="drawing" width="500"/>

>Hoeveel valid hosts?   
2ˆ(hoeveelheid host bits) - 2 oftewel 2 ^ (32 - CIDR)   

dingetje:
https://docs.google.com/document/d/1yKjb-4og1OYJi9eASbxUnoo3b4vJ4tG68oRhQd5vfMw/edit

