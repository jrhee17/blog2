---
layout: post
title:  "Using rxjs as an Ephemeral Storage for Mobile Applications"
date:   2019-01-30 20:41:24 +0900
categories: devnotes
---

## Problem Statement

# Purpose
We are developing a Bitcoin Alarm app which simply allows users to
- Add bitcoin alarms for a certain price
- Receive push notifications when a price is met

This is a contrived version of the overall flow of the app

![uml]({{ site.baseurl }}/assets/20190130/asisflow_uml.png)

A few notable points include
- Many REST api calls
    - This is a rapid prototyping app meaning requirements may change suddenly
- Websockets
    - This is for realtime ticker (coin price) updates and alarm triggers. Websockets are opened automatically on background -> foreground transition.

The following is a sample alarm list screen

![screenshot]({{ site.baseurl }}/assets/20190130/alarm_list.png)

A sample add alarm screen

![screenshot]({{ site.baseurl }}/assets/20190130/add_alarm.png)

Just in case anyone isn't familiar with crypto-jargon
- `exchange`: Entities (businesses) which trade cryptocurrency
- `coin`: Type of cryptocurrency (BTC, ETH , etc.)

# Problem
We would like to display `In-app-purchase to add more alarms`
(It's unfortunate, but with server costs going out every month, every developer has to make *some* money)

The condition for which we would like to display this is
1. 3 alarms are already added
    - Saved in server -- can retrieve by REST [GET] `/alarms`
2. The user has not purchased the app
    - Saved in server. To decide if also need to save in client

- Note: Obviously we would also have to check whether the user has purchased this feature when the alarm is actually added.
This check is just to notify users before the actual purchase.

# Points to consider

1. I would like to be able to maintain control over how alarms are added
    - What if I want to change the number of free alarms from `3` to `5` without app deployment?
2. I would like to minimize storage from the client side
    - What if I want to get rid of this add-alarm-restriction? Will there be useless client data/code?
    - Data inconsistency always happens between server and clients
3. I would like to still maintain some efficiency
    - Should try to avoid calling the same api multiple times in different screens
4. I'm all for asynchronous everything, but flickering screens are not good for UX
5. I would like a generalized pattern (redux???) that can handle calls like this
    - Unfortunately, while using `react-navigation` with `react-native`, `react-redux` isn't an option.

# Possible solutions
With the above points in mind, I drafted the following 4 possible solutions

**Pass Parameters**

![uml]({{ site.baseurl }}/assets/20190130/passparams_uml.png)

**Rest Call Every Time**

![uml]({{ site.baseurl }}/assets/20190130/rest_uml.png)

**Websocket Call**

![uml]({{ site.baseurl }}/assets/20190130/socket_uml.png)

**RXJS cached variant**

![uml]({{ site.baseurl }}/assets/20190130/cached_uml.png)

![]({{ site.baseurl }}/assets/20190130/new_standard.jpeg)

