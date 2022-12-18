---
layout: post
read_time: true
show_date: true
title:  How to monitor azure event hub events in real-time?
date:   2022-12-13 08:00:00 +0100
description: Azure event hub, service bus explorer, monitor, real-time
img: posts/uncategorized/azure.png
tags: [Azure]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-monitor-azure-event-hub-events-in-real-time.html'
---

When you are debugging your application and you want to monitor the event in real-time, you can use **service bus explorer**.

![](./../../../assets/img/posts/2022-12-13-azure-event-hub/service-bus-explorer.png)

<!--more-->
<br>

Firstly, download [service bus explorer](https://github.com/paolosalvatori/ServiceBusExplorer) from github and unzip it.


Then, find out the connection string with the following path on azure portal.
"the event hub to monitor" => "Settings" => "Shared access policies" => "Policy" => "Connection string-primary key"

And, add connect to the event hub by pasting the chosen connection string.

![](./../../../assets/img/posts/2022-12-13-azure-event-hub/connect_event_hub.png)

Choose any consumer group of the event hub

![](./../../../assets/img/posts/2022-12-13-azure-event-hub/consumer_group.png)

And right-click the consumer group to create a listener

![](./../../../assets/img/posts/2022-12-13-azure-event-hub/consumer_group_listener.png)

Now you'll see the listener interface

![](./../../../assets/img/posts/2022-12-13-azure-event-hub/consumer_group_listener_interface.png)

Choose "ZipEventDataInspector" and "Tracking" and the "Starting Date Time UTC" and click "Start" before your debugging.

![](./../../../assets/img/posts/2022-12-13-azure-event-hub/monitor.png)

Once you have sent the message to the event hub you're listening, you will see the message displayed here.

![](./../../../assets/img/posts/2022-12-13-azure-event-hub/event_message.png)

