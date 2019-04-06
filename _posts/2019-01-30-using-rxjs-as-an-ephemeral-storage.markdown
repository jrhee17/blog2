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

1. I would like to be able to maintain control over how alarms are added from the server side
    - What if I want to change the number of free alarms from `3` to `5` without app deployment?
2. I would like to minimize storage from the client side
    - What if I want to get rid of this add-alarm-restriction? Will there be useless client data/code?
    - Data inconsistency always happens between server and clients
3. I would like to still maintain some efficiency
    - Should try to avoid calling the same api multiple times in different screens
4. I'm all for asynchronous everything, but flickering screens are not good for UX
5. I would like a generalized pattern (redux???) that can handle calls like this
    - Unfortunately, while using `react-navigation` with `react-native`, `react-redux` isn't an option.
6. Minimize number of server apis if possible

# Possible solutions
With the above points in mind, I drafted the following 4 possible solutions

**Pass Parameters**

![uml]({{ site.baseurl }}/assets/20190130/passparams_uml.png)

*Description*
- Simply call `navigate(routeName, params)` with alarm list as params

*Cons*
- Always have to retrieve alarm list before navigating to add alarm screen
- Domain-wise Add-Alarm screen has little to do with already added alarms
- Hard to control add-alarm policy

*Pros*
- Simple and straightforward to achieve
- Efficient - no extra server calls


**Rest Call Every Time**

*Description*
- Call `[REST] GET alarm/addable` every time add alarm screen is loaded

*Cons*
- REST call every time page is loaded
- Need to create a non-restful api

*Pros*
- Simple and straightforward to achieve
- Easy to control add-alarm policy

![uml]({{ site.baseurl }}/assets/20190130/rest_uml.png)

**Websocket Call**

![uml]({{ site.baseurl }}/assets/20190130/socket_uml.png)

*Description*
- Send `{'type': 'check.alarm.addable'}` every time add alarm screen is loaded

*Cons*
- Minimal efficiency advantage over Rest call (assuming HTTP/2)
- Hard to develop good UI for asynchronous result 

*Pros*
- no real advantage

**RXJS cached variant**

![uml]({{ site.baseurl }}/assets/20190130/cached_uml.png)

*Description*
- Cache api calls using redux pattern and use cached to determine whether alarm is addable 

*Cons*
- Challenging to implement
- Can't control logic from server

*Pros*
- Efficient - no extra server calls
- Generic - no extra api calls
- Client won't be saving anything.
Whenever app dies, all data will be reset.

# Final Verdict

I have decided to go with **Redux pattern using RXJS** because I believe it will be worth the hassle.
In my head, it will go something like this...

*EphemeralStorage*
```javascript
class EphemeralStorage {
    constructor() {
        this.alarmListSubject = new Rx.BehaviorSubject([]);
    }
    async updateAlarmList() {
        const alarmList = await RestClient.getJson(`/alarms`);
        this.alarmListSubject.next(alarmList);
    }
    getAlarmListSubject() {
        return this.alarmListSubject;
    }
}
export default new EphemeralStorage();
```

*AlarmList Screen*
```javascript
class AlarmList extends React.Component {
    
    componentDidMount() {
        EphemeralStorage.getAlarmListSubject().subscribe(alarmList => this.setState({alarmList}));
        this.fetchAlarmList();
    }
    
    fetchAlarmList() {
        EphemeralStorage.updateAlarmList();
    };
}
```

*AddAlarm Screen*
```javascript
class AddAlarm extends React.Component {
    checkAlarmAddable() {
        EphemeralStorage.getAlarmListSubject().subscribe((alarmList) => {
            this.setState({
                addable: alarmList.length === 3 && purchased,
            })
        })
    };
}
```

NOTE: Please don't trust the code I have just written above -- it is pseudocode that kind of spiralled out of control.

Also, some more considerations

1. Need to make actions more readable (possibly make it more redux-esque)
2. Not entirely comfortable using rxjs, so I'll need to go through the documentation again (for the 20th time...)

When I'm done with this task, hopefully I'll be able to give some updates whether I still think this was the right decision.

![]({{ site.baseurl }}/assets/20190130/new_standard.jpeg)

