---
title: Event-driven Architecture
---
Event triggers and communicates between decoupled services. It is common in modern applications built with [[Microservices]].
- An event is a change of state that can be recorded by an app and shared with another app

Event-driven architecture, which pushes information as events happen, is a better architectural approach than waiting for systems to periodically poll for updates.
- Could be Pub/Sub model and event streaming(written to a log)

When to use this architecture:
- Multiple subsystems must process the same events
- Real-time processing with minimum time lag
- Complex event processing, such as pattern matching or aggregation over time windows
- High volume and high velocity of data, such as IoT
