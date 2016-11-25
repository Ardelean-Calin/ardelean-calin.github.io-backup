---
layout: post
title: 'ESP8266 Weather Station'
categories: electronics embedded esp8266
tags: iot internet-of-things esp8266 bme280 weather 3d print
published: true
---

# **Introduction**


The **[ESP8266](http://www.esp8266.com/wiki/doku.php?id=getting-started-with-the-esp8266)**
is a really versatile device. A **less than 3$** internet-enabled microcontroller is 
a very good deal, having both Wi-Fi functionality, as well as a pretty powerful 80-160 MHz 
microcontroller with lots of flash storage, RAM, and with an on-board ADC, I2C interface,
SPI interface and timers. One doesn't really need an additional microcontroller to develop
their IoT application.

One commonly found application of such a chip is making a **Weather Station** which uploads
temperature, pressure and humidity to the cloud. 

**[My weather station](/weather)** was built using the **ESP8266** as the brain and the
**[BME280](https://ae-bst.resource.bosch.com/media/_tech/media/datasheets/BST-BME280_DS001-11.pdf)**
as an enviromental sensor to measure temperature, pressure and relative humidity.

Below you can find the **required parts**, a **block schematic** (a proper schematic wasn't really necessary
for such a simple design) and the **sources** (code and STL of the 3D case) required to build one of your own.

## **Parts List**

+ ESP8266 Wi-Fi chip
+ BME280 Environmental sensor
+ 2200 mAh Li-Ion battery
+ TP4056-based Li-Ion charger (PCB from eBay)
+ 1000uF 6.3V Electrolytic Capacitor (for handling the large current spikes when connecting to Wi-Fi)
+ MCP1825S 3.3V LDO Voltage Regulator (pretty high quiscent current -> 220uA)
+ Enclosure with "breathing holes" (3D printed, in my case)

## **Basic design**

<img src="https://i.imgur.com/z5Zrq2M.png" style="max-width: 100%">

## **Source Code**

*The source code, as well as 3D design files can be found at the following link* 

<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/ardelean-calin/ESP8266-BME280-Weather-Station" data-icon="octicon-star" data-style="mega" data-count-href="/ardelean-calin/ESP8266-BME280-Weather-Station/stargazers" data-count-api="/repos/ardelean-calin/ESP8266-BME280-Weather-Station#stargazers_count" data-count-aria-label="# stargazers on GitHub" aria-label="Star ardelean-calin/ESP8266-BME280-Weather-Station on GitHub">Star</a>

## **Finished Build**

<img src="http://i.imgur.com/fDnJt3z.jpg" style="max-width: 100%">

<img src="http://i.imgur.com/KCHDYAk.jpg" style="max-width: 100%">