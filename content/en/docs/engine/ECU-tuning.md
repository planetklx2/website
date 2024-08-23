---
title: ECU tuning
description:
weight: 2
---

The KLX250/KLX300 platform offers significant power increase potential with minimal (or no) investment in performance parts.

The basic principle is simple:

1. Improve airflow through the intake, head, and exhaust by removing bottlenecks.
1. Adjust fuel supply to match the increased airflow.

The first step involves hardware upgrades (see the [Intake](../intake) and [Exhaust](../exhaust) sections). 

The second step requires ECU tuning which consists two things:
1. [Fuel management](#fuel-tuning) (common approach)
1. [Advanced ECU tuning](#advanced-ecu-tuning) altering ignition timing

Please read through the entire article below for better understanding.

## Fuel Injection Basics

Let's take a step back to understand how basic fuel injection works.

The bike's ECU (computer) receives signals from various sensors and determines when and how much fuel to inject into the airflow for complete combustion in the cylinder.

How does the ECU know how much fuel is needed? The KLX250/KLX300 has an O2 sensor in the exhaust that measures oxygen levels. The ECU operates in two modes:

1. **Closed loop**: Uses O2 sensor readings to adjust fuel delivery.
1. **Open loop**: Ignores O2 sensor readings and relies on a pre-programmed fuel map.

### Open loop

Open loop is simpler. The ECU uses a fuel map (lookup table) based on sensor values to determine fuel injection amount. For example:
For example:
Inject 1g of gasoline if:
- Air temperature is 20 degrees
- Air pressure is 101 kPa
- RPM is 4000
- Manifold pressure is 50 kPa
- Throttle position is 50% open

Open loop operation is limited and less efficient than closed loop, as it can't adapt to varying conditions. It's primarily used at wide-open throttle (WOT) and idle.

### Closed Loop 

In closed loop, the ECU combines sensor readings (including the O2 sensor) with the fuel map to make real-time adjustments. It can increase or decrease fuel delivery by up to 20-30% based on the O2 sensor's feedback.

Ideally, the ECU would always operate in closed loop, eliminating the need for additional tuning. However, there are limitations:

- The O2 sensor needs time to warm up.
- The engine must be in a stable operating condition.
- WOT conditions use a dedicated fuel map, bypassing the O2 sensor.
- Sensor failures require fallback options.

## Fuel Tuning

Increasing intake, head, or exhaust airflow requires a corresponding increase in fuel. While the ECU can compensate to some extent in closed loop, it's insufficient for open loop conditions. Therefore, **additional fuel control is essential**.

There are two primary methods to control fuel on the KLX250/KLX300 with standard OEM ECU:

{{< alert type="warning" color="warning" title="Warning!" >}}
The "O2 delete" mod (replacing the O2 sensor with a resistor) is counterproductive. It tricks the ECU into adding excess fuel in closed loop but does nothing for open loop. This can lead to lean air-fuel mixtures, detonation, and engine damage.

Here's a more detailed explanation:
- **Closed loop reliance**: The O2 sensor is only active in closed loop. With the O2 sensor removed (replaced by a resistor), the ECU constantly thinks the engine is running lean (lacking fuel) and attempts to compensate by enriching the fuel mixture. This can lead to rich running (excessive fuel) in closed loop.
- **Open loop ineffectiveness**: The "O2 delete" mod has no effect on open loop operation. The ECU relies on the pre-programmed fuel map in open loop, which is not adjusted based on the nonexistent O2 sensor signal. If the increased airflow from intake/exhaust modifications is not matched by a corresponding fuel increase, the air-fuel mixture becomes lean, especially in open loop conditions.
- **Lean air-fuel mixture dangers**: A lean air-fuel mixture burns hotter than intended. This can cause detonation (uncontrolled combustion) that can damage pistons, rings, and valves.

{{< /alert >}}

| Technical Term   | Description                                                                                                                                                                                                                                                              |   |   |   |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---|---|---|
| Closed loop      | An engine operating mode where the ECU uses the O2 sensor signal to adjust the air-fuel mixture for optimal combustion.                                                                                                                                                  |   |   |   |
| Open loop        | An engine operating mode where the ECU relies on a pre-programmed fuel map to determine fuel delivery, without using the O2 sensor signal.                                                                                                                               |   |   |   |
| Air-fuel mixture | The ratio of air to fuel in the engine's combustion chamber. A stoichiometric air-fuel mixture is ideal for complete combustion, typically around 14.7 parts air to 1 part fuel. Lean mixtures have less fuel than ideal, while rich mixtures have more fuel than ideal. |   |   |   |
| O2 sensor        | An exhaust gas sensor that measures the oxygen content in the exhaust stream. The ECU uses this signal to determine whether the air-fuel mixture is lean or rich.                                                                                                        |   |   |   |
| Detonation       | Also known as knocking or pinging, detonation is uncontrolled combustion that occurs when the air-fuel mixture ignites prematurely in the cylinder due to high temperatures or pressure. Detonation can cause significant engine damage.                                 |   |   |   |
| ECU              | Electronic Control Unit, the engine's main computer that controls various functions including fuel injection, ignition timing, and emissions control.                                                                                                                    |   |   |   |
| Resistor         | An electrical component that resists the flow of current. In the context of the "O2 delete" mod, a resistor is used to simulate the O2 sensor signal, but it cannot replicate the dynamic signal of a functioning sensor.                                                |   |   |   |


### Replace injector

The stock injector has a flow rate of 220cc/min. A common upgrade is to replace it with a 270cc/min injector from a Suzuki GSX-R1000 (part number `15710-21H00`). This provides a 22.7% increase in fuel flow, which is roughly equivalent to the displacement increase from a KLX250 to a KLX300.

- **Pros**: Reliable, inexpensive (~$20).
- **Cons**: Limited control, adds a fixed amount of fuel across the entire RPM range.

### Piggyback Fuel Controllers

Piggyback controllers intercept the signal between the ECU and injector to adjust fuel delivery. They offer more precise control than simply replacing the injector, allowing for different fuel adjustments across different RPM ranges. Popular options include EJK and PowerCommander Fuel Controller (PCFC).

We recommend our own **PlanetKLX2 piggyback controller**, which features:
- Precise fuel management in three independent RPM ranges.
- Easy operation via Bluetooth mobile app.
- Rugged waterproof design.
- Plug-and-play installation.
- Low cost - $140 shipped worldwide. **If you need one - please see [Shop](../shop#fuel-controller) section.**

<iframe width="840" height="472" src="https://www.youtube.com/embed/6S4ZwMfnvck?si=loC3DFEnOL_YE6gM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


With correct air-fuel mixture(controlled with piggyback), removed subthrottle plate, free flowing full exhaust (with header) and open airbox (removed airbox cover and snorkel) KLX300 can produce about **28.5hp @ 7500rpm** (pink line on the chart below).

![](https://s3.amazonaws.com/cdn.planetklx2/images/klx250-300-snorkel-vs-lidless.jpeg)

## Advanced ECU tuning

While fuel tuning is essential it's not sufficient for really high performance KLX. As we discussed in [ECU limitations](./ecu/#rev-limiter) Kawasaki put "soft rev limiter" into ECU which limits top end power. 

We are aware of 3 ways to mitigate soft rev limiter

### Unrestricted KLX250 OEM ECU

Different countries impose different emission regulations. If we investigate KLX250 Service Manual we will discover that on the most of the markets:
1. Bike produce **22hp@7500** rpm
1. Ignition is BTDC 10° @1300 (rpm) to ∼ BTDC **34**° @11000 rpm

There are however **2 exceptions: Indonesia and Japan**. In these countries service manual states following:
1. Bike produce **24hp@9000** rpm
1. Ignition is BTDC 10° @1300 (rpm) to ∼ BTDC **39**° @11000 rpm

Things however are even more complicated. On a fresh (2016+?) Indonesian motorcycles ECU also have restricted ignition (tested on our own KLX250 2022).

We've been able to purchase several unrestricted Japanese & Indonesian ECUs and test on the dyno. Results are impressive - **30.93hp@8200rpm** (open airbox + full exhaust + removed subthrottle plate) and stable overrev power up to 10000rpm.

**If you need one - please see [Shop](../shop#unrestricted-ecu) section.**

Compare to the pink line which is standard KLX250 ECU (same mods - open airbox + full exhaust + removed subthrottle plate).
![](https://s3.amazonaws.com/cdn.planetklx2/images/klx300-jdm-ecu.jpg)



### ECU reflash

[Best Dual Sport Bikes (BDSB)](https://www.bestdualsportbikes.com/kawasaki-ecu-mapping) offers ECU reflash for KLX300 for $349. According to their dyno it shows nice power boost (~10%) over entire RPM range. With modified OEM echaust and additional holes in the airbox reflash offers about **25 peak hp**. Early customers feedback is very positive.

See below KLX300 dyno charts from BDSB:
1. Red - factory stock KLX300 with secondary throttle ("subthrottle") plate in place
1. Yellow - factory stock KLX300 with secondary throttle ("subthrottle") out
1. Orange - ECU reflash + modified exhaust + drilled airbox
![](https://static.wixstatic.com/media/be4f25_f91d15bf16b74f278caf214d434ca648~mv2.jpeg/v1/crop/x_0,y_0,w_1273,h_770/fill/w_1273,h_770,al_c,q_85,enc_auto/be4f25_f91d15bf16b74f278caf214d434ca648~mv2.jpeg)

{{< alert type="warning" color="warning" title="Warning!" >}}
Also we are **skeptical** about "top end" power in the BDSB dyno charts as **even stock motorcycle (yellow line) doesn't show same power loss** at 8000 rpm soft rev limiter as on other dyno charts. Likely BDSB use agressive "smoothing" on the power curves. Compare to a number of other dynocharts below:

<iframe width="560" height="315" src="https://www.youtube.com/embed/tw8LcXnG1vM?si=A55J0xDxa9XQvfTV&amp;start=212" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

![](https://s3.amazonaws.com/cdn.planetklx2/images/klx300-dirtrider-dyno-rev-limit.jpg)
![](https://www.cycleworld.com/resizer/YdJUY3lWwO32LBmNRD3WHfQT2v4=/1440x0/filters:focal(991x533:1001x543)/cloudfront-us-east-1.images.arcpublishing.com/octane/2YXOIH5QPRFEZPKDGMGRNH7ZNQ.jpg)
![](https://cimg6.ibsrv.net/gimg/www.kawasakiforums.com-vbulletin/1246x975/img_0226_75bd0d74ce7dae1d68214c13d790b13a5968173b_cb43fde679ebcc0751be212f37f9be4519a7bd73.jpg)
![](https://cimg7.ibsrv.net/gimg/www.kawasakiforums.com-vbulletin/1024x576/37329d94_65ac_41c2_9df6_488101fe6ea0_047f0b075f8fc915c0af5beab0b9c4772a24fc59_jpeg_6b0fcf820fd20c5f47c4115e031d6e9fe82c9ada.jpg)
{{< /alert >}}

### Aftermarket ECU

Thai company [Apitech](https://apitechth.com/) offers aftermarket ECU replacement for KLX250/KLX300. This is probably the most advanced solution as their standalone ECU provides complete engine management control including fuel management, ignition curves, throttle control, manifold pressure, etc.
The downside is that the software is not very intuitive and skilled engineers exist only in South East Asia. 
Also according to [Keng Engine](https://www.facebook.com/KengEngine/) (one of the "big bore" kit suppliers from Thailand) they stopped offer Apitech ECU to their customers due to poor reliability of their boards.