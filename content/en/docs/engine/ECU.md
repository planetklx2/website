---
title: ECU limitations
description: 
weight: 1
---

ECU on a motorcycle is a mini-computer which has many functions. In a context of engine performance ECU collects and process data from different sensors and controls fuel injection and ignition systems.

Apart from ignition timing and amount of fuel KLX's ECU also can limit amount of air comning to cylinder using subthrottle ("secondary throttle plate"). Subthrottle is a useful concept on big powerful bikes which might help ECU to not get you into trouble when you twist you hand too quick :-) But it's not so useful on a 300cc dual sport bike.

How does ECU limits power on KLX250/300? There are two main limitations.
1. [Airflow restriction with subthrottle](#subthrottle)
1. [Soft rev limit](#rev-limiter)

But don't get upset! We will discuss how to [defeat ECU limitations](../ecu-tuning)!

## Subthrottle

For some reason (emissions?) Kawasaki engineers decided to limit subthrottle opening even if main throttle fully open. Subthrottle operated exlusively by ECU and has no mechanical connection to motorcyle throttle tube.

On KLX300 this results in power drop at 5000 following spike at 7000 rpm when subthottle finally getting fully open:

![](https://s3.amazonaws.com/cdn.planetklx2/images/klx300-dirtrider-dyno-subthrottle.jpeg)

There is no such dramatic midrange torque & power drop on KLX250. But secondary throttle still limits the airflow. Please see red line on the dyno chart below (stock KLX250 without single modification):

![](https://s3.amazonaws.com/cdn.planetklx2/images/klx250-snorkel-dyno.jpg)


## Rev limiter

A lesser know fact is that Kawasaki implemented a soft rev limiter at 7500 rpm on KLX250 (most of the markets) and at 8000 rpm on KLX300. The detailed mechanism [is not fully studied, but likely following things happen](https://www.kawasakiforums.com/forum/klx-250s-71/stand-alone-tuning-ecu-klx250-36083/page3/#post450575) :
1. ECU limits airflow with subthrottle
1. ECU reduce voltage to ignition coil
1. ECU retards ignition

As a result we see a torque and hp cliff after 7500 (KLX250) and 8000 (KLX300) rpm:

![KLX250](https://s3.amazonaws.com/cdn.planetklx2/images/klx250-7500-drop.jpeg)
![KLX300](https://s3.amazonaws.com/cdn.planetklx2/images/klx300-dirtrider-dyno-rev-limit.jpg)

Please read [ECU tuning](../ecu-tuning) to learn how to mitigate this.