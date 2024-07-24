## Background

Many applications are capable of adjusting their bit rate based on
network conditions and attempt to understand what bitrate is usable for
a given network UDP 5-tuple. Some networks use rate-limiters to
influence these applications. However, when networks enforce
rate-limiters, applications like video streaming or conferencing
struggle to adapt, leading to a suboptimal user experience.

This WG aims to establish a mechanism for devices intending to
rate-limit a UDP 5-tuple to communicate the maximum allowable
bitrate—termed "application limit"—to the endpoint originating the UDP
5-tuple.


## Goals

This work will define a way for an application to:

1. Signal their ability to receive application limits for UDP 5-tuples
to network elements.

2. Receive notifications from network elements about the application
limits for both upstream and downstream traffic.

3. Allow network elements to update the application limit as needed.

The application limit serves as a guideline to enhance user experience
and represents the maximum bitrate manageable by a single network
element. It is not an indicator of network congestion. This mechanism
focuses on bitrate limits intended for adaptive bitrate applications and
operates independently of congestion control algorithms and mechanisms
like BBR, ECN, and L4S.

The working group will analyze the privacy and security implications of
the solution.

### Non-Goals

This working group will not produce a solution that: 

1. Looks inside a QUIC or TLS encryption envelope

2. Is appropriate for use as input to a congestion control algorithm

3. Provides information other than the application limit 


## Program of Work

The WG is expected to:

1. Develop a standards track protocol to communicate the maximum allowable
bitrate—termed "application limit"—to the endpoint.
2. Develop an Informational Applicability and Manageability specification.

The WG will work collaboratively with the WEBTRANS, MOQ, AVTCORE, MOPS,
QUIC, TSVWG,and CCWG WGs as appropriate.

