---
layout: post
title:  "Using rxjs as an Ephemeral Storage for Mobile Applications"
date:   2019-01-30 20:41:24 +0900
categories: devnotes
---

# Problem Statement

![Alarm List](/assets/20190130/alarm_list.png)

# What it boils down to

1. Will this data have to be retrieved every time?
    - Can this data be stored in the mobile application
2. Does this data have to be retrieved synchronously?
    - HTTP vs (Long Polling, Websockets, etc.)