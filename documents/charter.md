Video traffic is 70% of the overall traffic volume on the Internet and is expected to grow to 80% by 2028.
Across developed and emerging markets video traffic forms 50-80% of traffic volume on mobile networks.
New formats like short form videos have seen tremendous growth in recent years.
These growth trends are likely to increase with new populations coming online on mobile-first markets.

Local mobile radio conditions may constrain the maximum throughput for a given client, or be so volatile as to rapidly change the maximum throughput throughout the course of a session.
In addition, despite capacity augmentation work such as deployment of new generations or new bands of spectrum, capacity augmentation efforts are not keeping pace with growth in demand.
These network operators have found it faster and less expensive to invest in shaping (also called throttling) of video traffic on a per-flow basis, which negatively affects video stream quality.
This is done for both network management and business motivations.
Network operators cannot explicitly measure the degradation to end user quality of experience (QoE) caused by traffic shaping, making this approach open loop.

Video traffic usually employs adaptive bitrate (ABR) schemes to dynamically adjust the video quality (and thus the data rate) in response to changing network conditions.
Ideally, when a network operator performs traffic shaping, the ABR scheme should adapt the video quality in use to reflect the data rate allowed by shaping, and converge on a bitrate allowed by the shaper.
In practice this convergence is extremely difficult to achieve while maintaining a good user experience.
Application providers are even designing algorithms to detect the presence of such traffic shapers and estimate the targeted shaping rate, however, these algorithms are likely to be both inaccurate and complex.
Instead, it would be beneficial, for both the application provider and network operator, to signal network attributes to the application to self-adapt its video traffic to conform to the specified characteristics.
The application provider has the ability to measure end user QoE and therefore can self-adapt with QoE feedback.

L4S is a recently standardized mechanism where nodes in the network assist endpoints in discovering optimal sending rates through continous ECN feedback that gets interpreted by purpose built congestion control algorithms.
However, L4S in itself is not sufficient as a mechanism to communicate network properties relating to video self-adaptation.
L4S and ECN operates on RTT timescales, reflecting the current state of a network buffer, whereas the network properties relating to video traffic reflect policies that tend to be stable over orders of magnitude longer time scales. 
It is possible to construct an L4S capable traffic policer that marks packets that do not conform to some policy instead of dropping or queueing them, however such a policer is not explicitly distinguishable from a network node that experiences congestion. 
Furthermore, a signal consumed by the application layer allows for efficient bursting of video segments, with burst sizes controlled by the sending entity rather than on-path network policers.

L4S is a recently standardized mechanism where nodes in the network assist endpoints in discovering optimal sending rates through continuous ECN feedback, interpreted by purpose-built congestion control algorithms. 
However, L4S alone is not sufficient to communicate network properties related to video self-adaptation. 
L4S and ECN operate on RTT timescales, reflecting the current state of a network buffer, whereas the network properties related to video traffic reflect policies that tend to be stable over orders of magnitude longer timescales. 
It is possible to construct an L4S-capable traffic policer that marks packets that do not conform to some policy instead of dropping or queueing them. 
Such a policer is not explicitly distinguishable from a network node that experiences congestion. 
Furthermore, a more long-term signal that is consumed by the application layer allows for efficient bursting of video segments, with burst sizes controlled by the sending entity rather than on-path network policers. 

The Secure Communication of Network Properties (SCONEPRO) Working Group's primary objective is to specify an on-path protocol for securely communicating network properties to clients relevant to a given application, such as the maximum achievable throughput for a video. 
- The working group will initially focus on a solution that communicates the maximum achievable throughput for a video delivered from a server to a client, using QUIC connections carrying the application signaling traffic.
- Work to support TCP or other transport protocols may be considered later in the working group, however, these considerations shouldn't distract from support for video over QUIC. 
- Further use cases may be considered later in the working group, however, it is not assumed that future use cases must or can be addressed by the same protocol. In essence, any protocol specified by the working group should be tailored to solve a specific use case.

The properties of this mechanism are as follows:

1. Associativity with an application.
The network properties must be associated with a given application traversing the network, for example a video playback.
1. Single communication channel for both client initiation and network properties.
The communication channel is initiated by a client device, just as the end to end application flows are also typically initiated by a client. The same communication channel is used to provide network properties to the client.
1. Network properties sent from the network.
The network provides the properties to the client. The client might communicate with the network, but won't be providing network properties.
1. On-path establishment.
That is, no off-path element is needed to establish the communication channel between the entity communicating the properties and the client.
1. Optionality.
The communication channel is strictly optional for the functioning of application flows.
A client's application flow must function even if the client does not establish the channel.
1. Properties are not directives.
A client is not mandated to act on properties received from the network, and the network is not mandated to act in conformance with the properties.
1. Resilient to NAT rebinding, QUIC connection migration, and Multipath QUIC operation.
The mechanism will allow the communication channel to be resilient to NAT rebinding, as long as the client is still served by the same logical Communication Service Provider (CSP). Additionally, the mechanism must work with flows that utilize QUIC connection migration or Multipath QUIC, and be able to distinguish network properties from two or more paths.
1. Scalability.
The mechanism must be scalable and implementable by Internet infrastructure as it exists today, for example mobile network packet cores.
1. Security.
The mechanism will have the ability to invoke security mechanisms that provide confidentiality, integrity, and authenticity of the communication. The working group will consider the value and implications of different confidentiality modes of the communication.

The working group will consider [RFC 9419](https://www.rfc-editor.org/rfc/rfc9419.html) as a source of principles in the development of this mechanism, and will consider relevant lessons from past IETF work in Path Aware Networking from [RFC 9049](https://www.rfc-editor.org/rfc/rfc9049.html).

The working group will coordinate with other groups, both inside and outside the IETF, as work progresses. Some of these groups might be
* WEBTRANS (in the IETF, which coordinates with W3C, responsible for browser specifications and APIs)
* MOQ (producing a specification for streaming media over QUIC)
* AVTCORE (producing an RTP-over-QUIC specification for real-time media)
* MOPS (responsible for  discussion of video technology’s requirements of networking standards, as well as proposals for new uses of IP technology in video)
* QUIC or HTTPbis, (if the working group identifies requirements for protocols used by SCONEPRO)
* TSVWG and CCWG (if these working groups work on mechanisms that could be used in response to changes in SCONEPRO path properties)

The proposed deliverables for SCONEPRO are as follows:

* Develop a standard track "SCONEPRO protocol" to securely communicate network information to clients. Its contents might include

    * protocol requirements for the base "SCONEPRO protocol"
	* describe minimal reference architecture for SCONEPRO deployment
    * discovery mechanism (if required)
    * connection establishment, communication signaling and data format (container to share network information)
    * specify and justify privacy and security requirements

* Develop a standard track specification based on SCONEPRO protocol to communicate network properties applicable to streaming video from the SCONEPRO monitor to the client(s). Its contents might include

    * describe use case and motivation
	* specify the applicable network properties to be communicated to the client
    * specify exact encoding of each applicable network property in the SCONEPRO protocol container
	* specify considerations for reusing these network properties in other encapsulations

* Develop an Informational SCONEPRO Protocol Applicability and Protocol Manageability specification. Its contents might include

	* guidance to operators making the decision to offer a SCONEPRO service in their networks
	* assistance to operators in tuning and troubleshooting a SCONEPRO service
