# Kismet Wireless

A colleague introduced me to this software package and made a pretty good pitch. The following are notes taken while learning about Kismet and Kismet Wireless.

## Table of Contents

- [Overview](#overview)
- [Bits and Pieces](#bits-and-pieces)
- [Resources](#resources)
- [Footer](#footer)

## Overview

Kismet Wireless is based on the original Kismet network packet sniffing package. It focuses on 802.11-based LANs, and provides a large number of tools to passively detect and track network traffic.

## Bits and Pieces

Things I've discovered through random exploration so far.

Kismet is:

- A baseline for an IDS system
- Open Source: GPLv2 license.
- Receive-only: Will not pollute a WiFi network while in use.
- A WiFi "frame associator" for quick or deep analysis of network traffic and patterns.

Kismet suports the following features on 802.11 LANs:

- Detecting
- Sniffing
- Tracking
- Realtime data collection
- Data storage for historical query, reporting

Kismet Wireless has a REST API:

- JSON and 2 other payload formats
- Many endpoints are query-based for gathering information
- Some endpoints set configuration or start activities in motion

Considerations when preparing to use Kismet Wireless:

- Antenna types: Directional, omni, and polarization considerations.
- Operating mode(s)
- Channel challenges within a band: Bandwidths, channel count, channel contention.
- Encoding schemes of wired and wifi signals.

Which activity: Discovery or Tracking?

- Discovery: Finding available bands and channels, the network nodes in a channel, and the modes of operation in use including association and many other network transaction types.
- Tracking: Pinpoint a signal, node, etc, and maintain a feed of input from its activities, whether physically moving or still.

Reatime vs Historical Data:

- Relational DB can be used to store all captured traffic.
- Queries can be used (canned or custom? both?) to trace specific traffic from start-to-finish (replay), or get other statistics about the captured packets.

## Resources

- Project Home: [Kismet GitHub Repository](https://github.com/kismetwireless).
- Web Home: [Kismet Wireless](https://www.kismetwireless.net).

## Footer

- Return to [ContEd Index](./conted-index.html).
- Return to [Root README](../README.html).
