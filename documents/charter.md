## Background

Many applications are capable of adjusting their bit rate based on
network conditions and attempt to understand what bitrate is usable for
a given network UDP 5-tuple. Some networks use rate-limiters to
influence these applications. However, when networks enforce
rate-limiters, applications like video streaming or conferencing
struggle to adapt, leading to a suboptimal user experience.

This WG aims to establish a mechanism for network elements intending to
rate-limit a UDP 5-tuple to communicate an upper bound on achievable
bitrate termed "throughput advice" — to the endpoint originating the UDP
5-tuple. 

In the context of this charter, a "network element" is defined as anything on 
the path of a UDP 5-tuple that is capable of dropping or delaying packets.

## Open Issues for Investigation

The working group will determine the necessity of a client signaling mechanism
which might separately signal their capability of receiving throughput advice
and their receipt of throughput advice. The working group will also
determine the mechanism’s impact on user privacy. These investigations will
inform the decisions on whether to include such mechanisms in the protocol.

## Goals

This work will define a way for an application to:

1. Receive notifications from network elements about the throughput
advice for both upstream and downstream traffic.

2. Allow network elements to update the throughput advice as needed.

The throughput advice serves as a guideline to enhance user experience
and represents the maximum bitrate manageable by a single network
element. It is not a strict indicator of network congestion. This mechanism
focuses on bitrate advice intended for adaptive bitrate applications and
is not a replacement for congestion control algorithms and mechanisms
like BBR, ECN, and L4S.

The working group will analyze the privacy and security implications of
the mechanism.

### Non-Goals

This working group will not produce a solution that: 

1. Looks inside a QUIC or TLS encryption envelope

2. Is appropriate for use as input to a congestion control algorithm

3. Provides information other than the throughput advice 


## Program of Work

The WG is expected to:

1. Develop a standards track protocol to communicate an upper bound on
achievable bitrate — termed "throughput advice"— to the endpoint.
2. Develop an Informational Applicability and Manageability specification.

The WG will work collaboratively with the WEBTRANS, MOQ, AVTCORE, MOPS,
QUIC, TSVWG,and CCWG WGs as appropriate.

