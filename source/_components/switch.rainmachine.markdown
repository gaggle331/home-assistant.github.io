---
layout: page
title: "RainMachine Switch"
description: "Instructions on how to use RainMachine units with Home Assistant."
date: 2017-08-04 12:00
sidebar: true
comments: false
sharing: true
footer: true
logo: rainmachine.png
ha_category: Switch
ha_iot_class: "Cloud Polling"
ha_release: 0.51
---

The `rainmachine` switch platform allows you to control programs and zones within
a [RainMachine smart Wi-Fi sprinkler controller](http://www.rainmachine.com/).

## {% linkable_title Configuring the Platform %}

The platform allows for either local (i.e., directly across the LAN) or remote
(i.e., through RainMachine's cloud API) access; the route you choose will
dictate what your configuration should look like.

For local access, specify the IP address/hostname of your RainMachine unit
and your RainMachine password:

```yaml
switch:
  platform: rainmachine
  ip_address: 192.168.1.100
  password: my_password_123
```

For remote access, specify your RainMachine username/email and password:

```yaml
switch:
  platform: rainmachine
  email: user@host.com
  password: my_password_123
```

Configuration Variables:

- **ip_address** (*Optional*): The IP address of your RainMachine unit
- **email** (*Optional*): Your RainMachine username/email
- **password** (*Required*): Your RainMachine password
- **zone_run_time** (*Optional*): The number of seconds that a zone should run when
turned on; defaults to 600 (10 minutes)

## {% linkable_title Controlling Your Device %}

After Home Assistant loads, you will see new switches for every enabled program
and zone. These work as expected:

- Program On/Off: starts/stops a program
- Zone On/Off: starts/stops a zone (using the `zone_run_time` parameter to
determine how long to run for)

Programs and zones are linked. If a program is running its final zone, you will
see both the program and zone switches turned on; turning either one off will
turn the other one off (just like in the web app).

## {% linkable_title Weblink %}

If you would like to see and control more detailed information, create an [iFrame](/components/panel_iframe/) that renders the RainMachine web app:

```yaml
panel_iframe:
  rainmachine:
    title: RainMachine
    url: "https://my.rainmachine.com/s/<YOUR_DEVICE_ID>/ui/"
    icon: mdi:water-pump
```

You can find `<YOUR_DEVICE_ID>` by logging into [https://my.rainmachine.com](https://my.rainmachine.com ) and taking note of the URL.

## {% linkable_title For Awareness %}

The remote RainMachine API currently has two broken operations (i.e., they return
error codes): starting a program and stopping a program. Please note that
starting/stopping programs with the remote API is disabled until RainMachine
can fix the issue.
