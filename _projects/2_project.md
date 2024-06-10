---
layout: page
title: Distributed MQTT Broker
description: A distributed MQTT broker that can be used to scale up the MQTT broker to handle a large number of clients, ensuring fault tolerance.
img: assets/img/mqtt.png
importance: 5
category: Featured
---

## AstraMQ : Distributed MQTT Broker: A Load-Balanced Redis-based Architecture

## Abstract
The Internet of Things (IoT) has revolutionized data transfer in industries through the MQTT protocol. MQTT is a lightweight messaging protocol designed for efficient communication among IoT devices, operating on a publish-subscribe model. Traditional single-node MQTT brokers face scalability and fault tolerance issues. This paper proposes a load-balanced Redis-based architecture for distributed MQTT brokers to address these limitations, ensuring scalability, redundancy, load balancing, and fault tolerance suitable for large-scale IoT deployments.


## Proposed Architectural Pattern for Distributed MQTT Broker

![System Architecture](https://github.com/RohanDoshi21/gRPC-Chat-Server/assets/63660267/8e7993ac-0747-45fa-b514-c838ffa99bfd)

### Key Components
1. **Load Balancer**:
   - Distributes incoming packets/messages to various broker nodes using a round-robin algorithm.
   - Ensures no single broker becomes a point of failure by evenly distributing the load.

2. **Redis**:
   - Acts as a global shared memory to store client state information and subscription tables.
   - Updated only when a client connects, disconnects, or subscribes to a particular topic.
   - Stores inflight messages with a Time-To-Live (TTL) ensuring message delivery to intended clients via any broker.

3. **Gossip-based Protocol**:
   - Utilized for discovering new nodes in the system, ensuring dynamic membership changes and fault tolerance.
   - Nodes share information at regular intervals to maintain system consistency over time.
   - Implemented using Hashicorp Memberlist Library for cluster management and failure detection.

### Architecture Overview
- Clients can connect to any broker in the cluster and consume subscribed topics.
- Brokers fetch updated client state and subscription information from Redis for message processing.
- Each publish message is broadcast to all other brokers through Redis streams, ensuring message delivery to subscribers and avoiding loops.

### Benefits
- **Scalability**: Enhanced client connectivity and load balancing improve system scalability.
- **Fault Tolerance**: Distributed components and load balancing ensure system robustness and fault tolerance.
- **Reliability**: Consistent client state and shared memory mechanisms contribute to a more reliable system.

## Implementation Details

### Client Distribution
- Clients can connect to any broker, maintaining persistent client state across the network.

### Subscription Distribution
- A global store of subscription state information (centralized or distributed) ensures efficient data delivery to subscribers.

### Message Distribution
- Load balancer distributes messages evenly across brokers, preventing any single point of failure.

