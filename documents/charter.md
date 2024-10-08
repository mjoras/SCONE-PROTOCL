## Background

Many applications are capable of adjusting their bit rate based on
network conditions and attempt to understand what bitrate is usable for
a given network UDP 4-tuple. Some networks use rate-limiters to
influence these applications. However, when networks enforce
rate-limiters, applications like video streaming or conferencing
struggle to adapt, leading to a suboptimal user experience.

## Goals

This WG aims to establish a mechanism for network elements capable of
rate-limiting a UDP 4-tuple to communicate an upper bound on achievable
bitrate termed "throughput advice" to the sender of packets matching 
the UDP 4-tuple.

This mechanism will allow an application to receive notifications
containing throughput advice for both upstream and downstream traffic
from any network elements capable of dropping or delaying packets on the
path of a UDP 4-tuple.

The throughput advice serves as a guideline to enhance user experience
and represents the maximum bitrate manageable by a single network
element. It is not a strict indicator of network congestion. This
mechanism focuses on throughput advice intended for adaptive bitrate
applications and is not a replacement for congestion control algorithms
and mechanisms like BBR, ECN, and L4S.

This mechanism will allow network elements to update the throughput
advice as needed.

The working group will analyze the privacy and security implications of
the mechanism.

In order to achieve the goals listed above, the working group will
determine whether it is necessary for an endpoint to explicitly signal
its capability of receiving throughput advice, and whether it is
necessary for an endpoint to confirm its receipt of throughput advice.

The working group will initially focus on developing a solution for
QUIC.

### Non-Goals

This working group will not produce a solution that:

1. Looks inside a QUIC or TLS encryption envelope

2. Is appropriate for use as input to a congestion control algorithm

3. Provides information other than the throughput advice

## Program of Work

The WG is expected to:

1. Develop a standards track protocol to communicate an upper bound on
achievable bitrate — termed "throughput advice"— from network elements
to the endpoint.

2. Develop an Informational Applicability and Manageability
specification.

The WG will work collaboratively with the WEBTRANS, MOQ, AVTCORE, MOPS,
QUIC, TSVWG,and CCWG WGs as appropriate.

The WG will coordinate its work with owners of any APIs that use
the "throughput advice" in order to ensure that browser applications will be able to
use SCONE protocol effectively, but no work on APIs will be carried out in the
working group.

## Milestones

- Submit a standards track protocol to communicate "throughput advice"— from network elements
to the endpoint to the IESG for publication by end of 2025.
- Submit an informational documentation of Applicability and Manageability for SCONE protocol to the IESG for publication by the end of 2025. 
