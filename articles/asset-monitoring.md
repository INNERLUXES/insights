# Asset Monitoring: How to Build a System People Actually Watch

*By Arsalan, Project Manager and IoT Expert, INNERLUXES. First published 6 September 2026 on [innerluxes.dev](https://innerluxes.dev/asset-management/asset-monitoring). That page is the canonical version; this file is the Markdown source.*

Asset monitoring explained by an IoT project manager who ships these systems: what to instrument, how to get data off the asset, alerts nobody learns to ignore, dashboards, IT asset monitoring, and what it takes to run.

*Arsalan runs asset monitoring projects at INNERLUXES. This is the version of the conversation he has with every client in week one, written down so you can read it before the kickoff call rather than after the first invoice.*

Most asset monitoring projects I have joined were not started because someone wanted data. They were started because something expensive stopped working and nobody could say why. A compressor seized on a Friday night. A refrigerated trailer lost temperature between two depots and the load was written off. A generator ran out of fuel in the one week it was the only thing keeping a site online.

After that, somebody asks for monitoring, a vendor sells sensors, dashboards appear, and eighteen months later those dashboards are open on nobody’s screen. The system was built. It just was not watched.

That gap is what this article is about. Not the sensors, which are the easy part now, but the decisions around them that determine whether anyone acts on what you paid to collect.

![Asset monitoring: from sensor to alert to the person who acts on it](https://innerluxes.dev/assets/icons/hero-condition-monitoring-software-style-icon.jpg)

## What asset monitoring actually means

The phrase covers two jobs that get confused constantly, and confusing them wastes real money.

**Physical asset monitoring** is watching equipment you own or are responsible for: pumps, motors, chillers, vehicles, tanks, generators, cold storage, medical devices out in the field. You attach something that measures, you get the readings back, and you do something when they go wrong. This is where the phrase came from and it is still what most people mean by it.

**IT asset monitoring** is watching the servers, endpoints, licences, certificates and cloud resources a business runs on. Different sensors, different failure modes, same underlying question: what do we own, is it healthy, and who is responsible when it is not. There is a section on that further down, because the differences matter more than the similarities.

A third thing gets sold under the same name and is not monitoring at all. [Real-time asset tracking](https://innerluxes.dev/asset-management/real-time-asset-tracking) answers where a thing is, rather than how it is doing. Plenty of businesses need both. They are separate builds with separate costs, and a supplier who quotes one while you are asking for the other is a supplier you will argue with later.

## Decide these before you buy a single sensor

I once watched a client buy four hundred sensors before deciding who would answer the alerts. They sat in a store room for eleven months. Now I refuse to start hardware selection until four questions have written answers.

- **What decision will this data change?** Not what will it show. What will somebody do differently. If the honest answer is that a technician gets sent out a day earlier, good, that is a real answer and it tells you exactly what accuracy and what latency you need. If the answer is that management would like visibility, stop and go find the decision, because visibility does not pay for a system.
- **Who is on the other end at three in the morning?** An alert with no owner is a log line. Before anything is instrumented, name the role that receives it, the hours they work, what they are authorised to do, and who they escalate to. If nobody is on at three in the morning, you have just learned that overnight alerts should queue rather than push, and that changes the whole design.
- **What is the asset worth when it fails?** Downtime, spoilage, a missed contractual window, a safety incident, a regulator. Put the consequence in words. A chiller holding vaccine and a chiller holding soft drinks deserve very different systems, and the second one does not deserve the first one’s budget.
- **Who owns the asset once it is instrumented?** Maintenance, operations, IT, or a leasing company. Whoever owns the asset has to own the monitoring, or the alerts land somewhere that cannot act on them.

These four answers go into a one page brief that the client keeps. Everything after this, hardware, connectivity, software and the running cost, is derived from that page. It is also the document our fixed price is written against, which is only possible because it exists.

## What to measure, and what to leave alone

Sensors are cheap enough now that the temptation is to measure everything and sort it out later. That is how you end up paying every month to store numbers nobody has ever queried.

The useful discipline is to work backwards from failure. Ask the maintenance team how each asset actually breaks, in their words, and you will usually get three or four modes per asset type. Bearings go before motors do, and they announce it in vibration. Belts slip and show up as a temperature rise downstream. Filters clog and show as a pressure difference. Batteries die slowly and show as a longer recharge curve, months before they strand a vehicle.

Instrument those. Vibration, temperature, pressure, current draw, run hours, door state, tank or fuel level, humidity for anything perishable. Then add the two boring ones that almost every system forgets: **is the sensor itself alive**, and **is the gateway still reporting**. A silent sensor looks exactly like a healthy asset, and that is the single most common way an asset monitoring system fails without anyone noticing.

Leave alone the things you cannot act on. If you have no plan and no budget to respond to a reading, collecting it is a cost with no return. You can always add a channel later. Removing one after operations has grown attached to a chart is much harder.

## Getting the data off the asset

This is where projects slip, and almost always for physical reasons rather than software ones. The site survey is not optional. I have seen a design built around cellular coverage that a basement plant room did not have, and a wired plan that would have needed a cable run through a fire door.

- **Wired, where the asset never moves and power is already there.** Cheapest to run, most reliable, and boring in the best sense. Industrial equipment with an existing control network usually falls here, and the job becomes reading from the controller rather than adding sensors at all.
- **Short-range wireless to a gateway** for dense clusters: a plant floor, a warehouse, a hospital wing. One backhaul connection serves many devices, and battery life runs to years if you are honest about how often you actually need a reading.
- **Cellular** for anything that moves or sits alone: vehicles, trailers, remote tanks, cabinets in the field. Budget the data plan across the whole fleet and the whole life of the asset, because that number surprises people far more than the hardware does.
- **Long-range low-power** for large sites where you need small readings from far away and can accept minutes rather than seconds. Farms, quarries, utilities, campuses.

Whatever you pick, design for the connection being down. Readings buffer on the device, they carry their own timestamp, and they go up when the link returns. If timestamps get applied at the server instead, a truck that drives through a tunnel produces a chart that lies to you, and you will not find that out until an investigation depends on it.

## Where the data goes once it arrives

The shape that has served our clients well is unremarkable, and unremarkable is the point.

Readings land on a broker that does nothing but accept and acknowledge them, so a burst of traffic never loses data. They are written into a time series store, which is the right tool for numbers with timestamps and costs a fraction of what a general purpose database costs at the same volume. Recent data stays at full resolution, because that is what you investigate with. Older data is rolled up to averages and extremes, because nobody needs a reading every ten seconds from two years ago, and keeping it is a bill you pay every month forever.

Rules run beside the store rather than inside the dashboard. This matters more than it sounds. If your alerting logic lives in the charting tool then nobody can test it, nobody can review it, and it quietly breaks the day someone edits a panel. Kept separate, the rules are code, they go through review, and they can be replayed against last year’s data to see how often they would have fired.

All of it sits in your own cloud account under your own billing. We build it there, we hand it over there, and leaving us does not require a migration. That is a deliberate choice, and it is how we approach [custom software development](https://innerluxes.dev/software-development/custom) generally.

## Alerts people do not learn to ignore

If you take one thing from this article, take this. An asset monitoring system is judged entirely by its alerts, and bad alerts are bad in the same three ways.

**They fire on a single reading.** Sensors are noisy. A threshold crossed once is usually nothing. Require the condition to hold for a period, or require several readings to agree, and most false alarms disappear before anyone gets woken up.

**They are absolute when they should be relative.** A motor running warm in July is not the same as the same motor running warm in January. Comparing an asset against its own recent behaviour, or against the identical units next to it on the same line, catches real problems earlier and shouts far less.

**They all arrive at the same importance.** If everything is urgent then nothing is. We use three levels, and we make the client write the sentence for each one: what it means, who it goes to, and what that person is expected to do within what time. A level nobody can write that sentence for is a level that should not exist.

Then there is the part almost nobody builds and everybody needs. Every alert should be acknowledged by a person, and every acknowledgement should record what they found. Six months of that turns into the only honest answer to the question that pays for the whole system: which of these alerts were worth having. Rules get tuned from that record. Without it, tuning is guesswork, and the alerts drift back into noise.

## Dashboards and the people who read them

Three audiences, three screens, and mixing them is why dashboards go unopened.

The technician needs one asset at a time: current state, the last day of readings, open alerts, what was done last time, and the manual. On a phone, in a plant room, with gloves on. Large targets, few taps, and it has to work on bad wifi.

The supervisor needs the fleet: what is red now, what is trending the wrong way, what is due for service this week. One screen, no scrolling, readable from across a room.

The manager needs the month: how much unplanned downtime, which assets caused it, how alerts are trending, what maintenance was deferred. This one can be an emailed report, and usually it should be, because that gets read.

Build the technician screen first. If the people closest to the asset do not use the system, the numbers on the manager’s report are made of nothing.

## IT asset monitoring is a different job

Everything above assumes an asset you can put a sensor on. When the asset is a server, a laptop, a licence or a certificate, the sensors already exist and the hard part moves somewhere else entirely.

With IT assets the failure is rarely that you missed a reading. It is that you did not know the asset existed. The laptop nobody returned when they left. The virtual machine spun up for a trial and still billing. The certificate that expires on a Saturday. The backup job that has been failing quietly since a firmware update in spring. None of those are monitoring failures. They are inventory failures wearing a monitoring costume.

So the first job is a complete list with a named owner against every line, and monitoring gets layered on top of it. We publish the check we run at the start of every engagement, which reads an estate inventory and reports what is unprotected, unowned or expiring: [github.com/INNERLUXES/it-estate-check](https://github.com/INNERLUXES/it-estate-check). It is deliberately small and readable so a client’s own team can run it without us.

After that, the monitoring itself is well trodden ground: availability, capacity, patch state, backup success proven by an actual restore, certificate expiry, licence renewal, and identity hygiene. If you would rather that ran as a service than as a project, that is what [managed IT services](https://innerluxes.dev/it-operations/managed) covers, and the estate inventory is the first three weeks of it.

## Buy a platform or build your own

I have no loyalty here. We build custom systems and we also integrate the big platforms, and I have talked clients out of a build more than once.

**Buy** when your assets are standard, the vendor already supports them, and what you want is what the platform does out of the box. You will be running within weeks. Read the licensing carefully, because per asset per month gets expensive at fleet scale, and check what happens to your history if you leave.

**Build** when the monitoring has to live inside something else you run. That is the common case in practice. Alerts have to raise work orders in your maintenance system, readings have to sit next to production records, customers have to see their own equipment in your portal, or the data feeds a model you own. Platforms handle those through integrations that are always thinner than the demo suggests.

**Build** also when the assets are yours and unusual. Custom machinery, a device you manufacture, a process nobody else runs. Off the shelf has no concept of your failure modes, and teaching it is often more work than starting clean.

The honest middle path, and the one we use most, is a bought platform for ingestion and storage with a custom layer for rules, workflow and the screens people actually use. You skip the boring infrastructure and keep control of the parts that carry your business logic.

## What it takes to run, year after year

Nobody asks about this at the start and everybody asks about it in year two.

- **Batteries and calibration.** Wireless sensors die. Put replacement into the maintenance schedule from day one, or coverage decays quietly and the system stops being trustworthy without ever appearing broken.
- **Alert tuning.** Plan a review each quarter using the acknowledgement record. Rules that never fire and rules that always fire are both telling you something.
- **Storage growth.** Decide the rollup and retention policy before launch, and revisit it yearly. This is the line item that grows on its own.
- **Firmware and platform updates.** Devices in the field need a safe update path, and that path needs testing on a small group before the fleet, exactly like any other release.
- **New assets.** Adding one should be a form, not a project. If it needs an engineer, adoption stalls at whatever was instrumented on day one.
- **The person who owns it.** Name them. A monitoring system with no owner is on a countdown from the moment it goes live.

None of this is exotic. It is just the part of the work that does not appear in a proposal unless somebody insists, and we would rather insist now than explain later.

## Questions clients ask us

**How long before we see anything useful?** A pilot on a handful of representative assets takes weeks, not months, and it is the right way to start. You learn what your data actually looks like, which is never quite what the design assumed, and you learn whether the people receiving alerts respond to them. Rollout after a pilot is mostly logistics.

**Can you work with the sensors we already bought?** Usually. If they can be read over a documented protocol or an API, we can bring them in. Tell us the makes and models before the design, because a closed device that only reports into its own vendor cloud will shape what is possible.

**Does this predict failures?** Eventually, and only if you earn it. Prediction needs a history of readings paired with a record of what actually failed and when. Most clients do not have that on day one. Build the monitoring and the acknowledgement record first, and in a year you will have the dataset that makes prediction a real project rather than a slide.

**Who owns the data?** You do, in your own cloud account, from day one. We do not host your readings on our infrastructure and we do not keep a copy.

**What should we do first?** Write the four answers from the section above. If you want a second opinion on them, send them over and you will get a written response with the architecture we would recommend and a fixed price within one business day. Related reading on this site: [enterprise asset management consulting](https://innerluxes.dev/asset-management), [condition monitoring for industrial equipment](https://innerluxes.dev/manufacturing/iot-for-condition-monitoring), [our IoT services](https://innerluxes.dev/iot), and [network monitoring](https://innerluxes.dev/it-operations/infrastructure/network-monitoring). The Markdown source of this article is public at [github.com/INNERLUXES/insights](https://github.com/INNERLUXES/insights).
