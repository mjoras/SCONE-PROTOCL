Video traffic is already 70% of the overall traffic volume on the Internet and is expected to grow to 80% by 2028.
Across developed and emerging markets video traffic forms 50-80% of traffic volume on mobile networks.
New formats like short form videos have seen tremendous growth in recent years.
These growth trends are likely to increase with new populations coming online on mobile-first markets.

Mobile network operators continuously invest in network resources, including deployment of new generations or new bands of spectrum.
Since spectrum is a limited and expensive resource, operators often make use of flow-based traffic handling such as shaping of video traffic, especially when the network is highly loaded.
Operators cannot explicitly measure the degradation that shaping causes to end user quality of experience (QoE), making this approach open loop. 

Video traffic usually employs adaptive bitrate (ABR) schemes to dynamically adjust the video quality (and thus the data rate) in response to changing network conditions.
In the presence of traffic shaping, the ABR scheme should ideally adapt the quality and converge on a bitrate sustainable by the shaper.
In practice this is extremely difficult to achieve while maintaining a good user experience.
Application providers are even designing algorithms to detect the presence of such traffic shapers and estimate the targeted shaping rate, however, these algorithms are likely to be both inaccurate and complex.
Instead, it would be beneficial, for both the application provider and network operator, to signal the shaper rate to the application to self-adapt their video traffic to conform to the specified characteristics.
The application provider has the ability to measure end user QoE and therefore can self-adapt with QoE feedback.

The Secure Communication of Network Properties (SCONEPRO) Working Group's primary objective is to specify an on-path protocol for securely communicating network properties to clients relevant to a given application, such as the maximum achievable bandwidth for a video. 
- The working group will initially focus on a solution that communicates the maximum achievable bandwidth for a video delivered from a server to a client, using QUIC connections carrying the application signaling traffic.
- Work to support TCP or other transport protocols may be considered later in the working group, however, these considerations shouldn't distract from support for video over QUIC. 
- Further use cases may be considered later in the working group, however, it is not assumed that future use cases must or can be addressed by the same protocol. In essence, any protocol specified by the working group should be tailored to solve a specific use case.

The properies of this mechanism are as follows:

1. Associativity with an application. 
The network properties must be associated with a given application traversing the network, for example a video playback.
1. Client initiation.
The communication channel is initiated by a client device, just as the end to end application flows are also typically initiated by a client.
1. Network properties sent from the network. 
The network provides the properties to the client. The client might communicate with the network, but won't be providing network properties. 
1. On-path establishment.
That is, no off-path element is needed to establish the communication channel between the entity communicating the properties and the client.
1. Optionality.
The communication channel is strictly optional for the functioning of application flows.
A client's application flow must function even if the client does not establish the channel.
1. Properties are not directives.
A client is not mandated to act on properties received from the network, and the network is not mandated to act in conformance with the properties.
1. Resilient to NAT rebinding. 
The mechanism will allow the communication channel to be resilient to NAT rebinding, as long as the client is still served by the same logical Communication Service Provider (CSP). 
1. Scalability.
The mechanism must be scalable and implementable by Internet infrastructure as it exists today, for example mobile network packet cores.
1. Security.
The mechanism must ensure the confidentiality, integrity, and authenticity of the communication.
The mechanism must have an independent security context from the application's security context.
The group must not define new security mechanisms for this purpose.

The working group will consider [RFC 9419](https://www.rfc-editor.org/rfc/rfc9419.html) as a source of principles in the development of this mechanism, and will consider relevant lessons from past IETF work in Path Aware Networking from [RFC 9049](https://www.rfc-editor.org/rfc/rfc9049.html).

The working group will coordinate with other groups, both inside and outside the IETF, as work progresses. Some of these groups might be
* WEBTRANS (in the IETF, which coordinates with W3C, responsible for browser specifications and APIs)
* MOQ (producing a specification for streaming media over QUIC)
* AVTCORE (producing an RTP-over-QUIC specification for real-time media)
* MOPS (responsible for  discussion of video technology’s requirements of networking standards, as well as proposals for new uses of IP technology in video)
* QUIC or HTTPbis, (if the working group identifies requirements for protocols used by SCONEPRO)
* TSVWG and CCWG (if these working groups work on mechanisms that could be used in response to changes in SCONEPRO path properties)
