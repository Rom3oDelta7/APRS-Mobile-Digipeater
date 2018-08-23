# Mobile APRS Digipeater ("MAD")
A self-contained portable APRS digipeater

## Introduction
APRS is the [Automated Packet Reporting System](https://www.aprs.oprg). It was created by Bob Bruninga, WB4APR, and subsequently grew to global proportions. 
APRS can be used to transmit and receive virtually any type of data, such as GPS position reports, telemetry data, weather data, and text messages.
What makes APRS different from using a mobile phone is that APRS uses amateur (ham) frequencies instead of cellular or Internet services.
A large network of APRS repeaters (aka digipeaters) operate similarly to the ham voice repeater network, with the important distinction that there is only a single frequency (no split).
(Note that the use of APRS requires an FCC amateur radio license).

Currently, the [Yavapai Amateur Radio Club](https://www.w7yrc.org "YARC") provides event communications for over a dozen public events each year in Yavapai County.
A large contingent of YARC members staff multiple stations along the course providing race status information, transportation requests for participants
who are unable to continue, and safety-related information such as vehicles trespassing on the closed course or participants in need of medical attention.
Many of these events are quite extensive, covering a large geographic area and encompassing well over one thousand participants.
These larger events, in particular, are outside of urban centers and cover such a widespread area that amateur radio is the only consistent means of communication for the event.
A key component to providing event communications is managing the course vehicles, which are typically provided by the event organizers
and staffed with a YARC member as a passenger to provide communications.
These vehicles handle logistics such as participant pickup, supplies and equipment, and “sweeping” the event to track the end of the race
and ensure that all participants get back safely.
This is a very dynamic situation with assignments frequently changing with the flow of the event.
As such, keeping track of the current location of these vehicles is critical to ensure the right vehicle is assigned to a given task.

Currently, our club is using mobile APRS transmitters in these vehicles to track their location.
APRS packets are received over a VHF frequency and decoded. 
The decided GPS information is used to plot the position on a map.
Internet services, such as https://aprs.fi can be used for tracking, but in our situation the Internet isn't available, so we use [UI-View] software instead.

While the aforementioned network of digipeaters vastly increases the coverage area for APRS, Yavapai County terrain can be vary significantly, resulting in coverage gaps especially
on the trails used for mountain bike and marathon events.
The portable APRS digipeater was designed and built to address this problem.
We use terrain mapping software([ubiquiti] or [radio mobile]) to determine the best location to cover the event area and we preposition the MAD before the start of the event.
Properly placed, the MAD will relay the packets from our tracking units to one of the 3 area mountaintop APRS digipeaters, enabling position reports to be received in our communications van.
To simplify deployment, everything is pre-programmed so all one needs to do is to attach an antenna and power it on.

We also plan to use this digipeater within our local [Yavapai County ARES/RACES emergency response group].

## A Mobile APRS Digipeater (MAD)
The MAD consists of a 12V power supply, APRS transceiver, an LCD display, a voltage regulator for the HT battery backpack, an 8W handitalkie (HT), and an SMA-F antenna mount.
I used the SMA-F mount to match our APRS mobile transceivers and enable antenna interchangeability (we use 1/4 wave and magmount antennas).
It is encased in a Pelican-like case with foam cutout spaces for the SLA battery, HT, and a 3D-printed control unit case.

[![MAD external view](https://github.com/Rom3oDelta7/APRS-Mobile-Digipeater/blob/master/Photos/MAD%20exterior.jpg)](https://github.com/Rom3oDelta7/APRS-Mobile-Digipeater/blob/master/Photos/MAD%20exterior.jpg)


The control unit housing contains the Byonics TinyTracker4 (TT4) transceiver, HT adapter cable, and a 4-line LCD to display decoded APRS messages.

### Case

The MAD is housed in an Apache 2800 12" IP65 weatherproof case.
There is a panel-mount PowerPole connection on the side that provides a direct connection to the 12V SLA battery, either for 12V out or to charge the battery.
On the top is an SMA-F antenna mount.

### Radio

I chose a Baofeng UV82HP HT for the radio. 
This HT is 8W, slightly higher than typical HTs.
I chose this unit since we have extensive experience with Baofeng and a lot of accessories on hand.
Also, Byonics (see below) makes a Baofeng-specific interface cable.
I did not program the radio, other than to set the 144.390 MHz APRS frequency and change/confirm a few settings:
* 0: SQL 5
* 2: power HIGH
* 3: SAVE OFF
* 4: VOX OFF
* 5: Wideband
* 6: 5 sec backlight timeout
* 7: TDR OFF
* 29: standby color OFF
* 30: RX color blue
* 32: TX color orange (RX & TX colors are useful when remotely troubleshooting with inexperienced operators)
* 35: STE OFF
* 39: Roger beep OFF

We keep the unit keyboard locked when in use.

### Control Unit

The control unit houses the [Byonics TT4 APRS transceiver], Byonics HTK2P [interface cable], and the [Byonics TT4 LCD display].
A mount is provided for the TT4 PCB, with adequate space to attach the interface cable inside the enclosure.
There is an opening for the DB9 serial connection required for programming.
You will need either a DB9 serial with null modem or a USB to serial adapter, e.g. FTDI (null modem), to configure the TT4.
Supposedly, a PS2 keyboard can be connected to the LCD adapter board and used to configure the TT4, but I did not verify that this approach works.
There are also 2 panel-mount PowerPole connections, one on the left side for power in, and one on the right to power the HT.
I used the Baofeng 12V battery adapter, but the voltage regulation electronics are in the 12V lighter socket assembly, and thus
useless in this application.
Instead, the 12V battery power is routed through a DC buck converter to reduce the voltage to 7.8V for the HT.
A Powerwerx PowerPole distribution hub is included to manage the power connections inside the enclosure.

The top has the power switch and the LCD display.
The switch controls the power from the external PowerPole connection to the distribution hub; switching it on turns on the power for
the TT4, HT, and display.

[![MAD internal view](https://github.com/Rom3oDelta7/APRS-Mobile-Digipeater/blob/master/Photos/MAD%20lid%20open.jpg)](https://github.com/Rom3oDelta7/APRS-Mobile-Digipeater/blob/master/Photos/MAD%20lid%20open.jpg)

When assembling the unit, manage your wire gauge and length carefully, as the case is a tight fit. 
I used 14 AWG wire is overkill given the low power draw, but that's what I had on hand and what would fit the crimped PowerPole connectors.
16 AWG would probably be a better choice, with the smaller gauge PowerPole crimp connectors, of course.

I chose to use the _assembled_ TT4 and the LCD display _kit_.
The rationale for this is that the assembled SMT board, unlike the through-hole (PTH) kit, has a header for the display unit.
If you use the TT4 PCH kit, you'll need to disassemble and strip the ends of the ribbon cable leads and solder the wires to the underside of the board.

#### Printing the Enclosure

There are no special requirements for printing the enclosure.
I used 0.4mm layers, with 2 solid bottom layers and 3 solid top layers (makes for better screw connections in the lid supports) on a Taz6.
I used high temperature PLA to avoid any issues with high temperatures that might cause standard PLA to deform (yes, it does happen).
You can either print the washer to secure the TT4 PCB to the case or just use a standard nylon or other non-conductive washer.

### Battery

The battery is a standard 12V sealed lead acid (SLA) battery, with a 5A blade fuse on the positive lead.
The battery is mounted upside down to simplify the wiring.
There are no special requirements for the battery, but I prefer the Keyko AGM gel batteries.




[ubiquiti]: https://airlink.ubnt.com/#/ptp
[radio mobile]: http://www.ve2dbe.com/rmonline.html
[UI-View]: http://www.ui-view.net/
[Byonics TT4 APRS transceiver]: https://www.byonics.com/tinytrak4
[interface cable]: https://www.byonics.com/ht_cables
[Byonics TT4 LCD display]: https://www.byonics.com/tinytrak4
[Yavapai County ARES/RACES emergency response group]: https://www.k7yca.org
