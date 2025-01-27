---
title: Synchronization Techniques
---
**latency**: time between receipt of a service request and the initiation of service. This can be both hardware/software or CPU latency/ Device latency

**real-time system**: guarantees a worst-case latency for critical events

two terms are used to define system performance: latency and throughput
- latency - time between the receipt of a service request and the initiation of service
- throughput - measure of how many requests can be serviced per unit of time

**synchronization mechanisms**
**cpu-oriented**
- blind cycle/blind synchronization: device status is not known; software waits for some time and then acts on the data even if the device was not ready
- occasional polling: device status is checked at convenience; checks repeat at "irregular" intervals until device is ready and in between checks, system performs other tasks
- periodic polling: device status is checked after pre-determined amount of time; checks repeat at regular intervals
**device-oriented sync**
- tight polling/ gadfly/ busy waiting: device status is continuously checked. no other tasks are being performed
- interrupt handling: device generates a hardware interrupt to request service immediately when device status changes

