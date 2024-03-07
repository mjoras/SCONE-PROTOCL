Video traffic is already 70% of the overall traffic volume on the Internet and is expected to grow to 80% by 2028.
Both in developed and emerging markets video traffic forms 50-80% of traffic volume on mobile networks.
New formats like short form videos have seen tremendous growth in recent years.
These growth trends are likely to increase with new populations coming online on mobile-first markets.

While mobile network operators continuously invest in network resources, including deployment of new generations or new bands.
Since spectrum is a limited and expensive resource operators often make use of flow-based traffic handling such as shaping of video traffic, specially when the network is highly loaded.
Operators can not explicitly measure the degradation that shaping causes to end user quality of experience (QoE) making this approach open loop. 

Video traffic usually employs adaptive bitrate (ABR) schemes to dynamically adjust the video quality (and thus the data rate) in response to changing network conditions.
In the presence of traffic shaping, the ABR scheme should ideally adapt the quality and converge on a bitrate sustainable by the shaper.
In practice this is extremely difficult to achieve while maintaining a good user experience.
Application providers are even designing algorithms to detect the presence of such traffic shapers and estimate the targeted shaping rate, however, these algorithms are inaccurate and complex.
Instead, it would be beneficial, for both the application provider and network operator, to signal the shaper rate to the application to self-adapt their video traffic to conform to the specified characteristics.
The application provider has the ability to measure end user QoE and therefore can self-adapt with QoE feedback.

The Secure Communication of Network Properties (SCONEPRO) Working Group's primary objective is to specify an on-path protocol for securely communicating network properties to clients relevant to a given application, such as the maximum achievable bandwidth for a video. 
- The working group will initially focus on a solution that communicates the maximum achievable bandwidth for a video using QUIC connections carrying those applications.
- Work to support TCP or other transport protocols may be considered later in the working group, however, these considerations shouldn't distract from support for video over QUIC. 
- Further use cases may be considered later in the working group, however, it is not assumed that future use cases must or can be addressed by the same protocol. In essence, any protocol specified by the working group should be tailored to solve a specific use case.

The properties of this mechanism are as follows:

1. Associativity with an application. 
The network properties must be associated with a given application traversing the network, for example a video playback.
1. Client initiation.
The communication channel is initiated by a client device, just as the end to end application flows are also typically initiated by a client.
1. On-path establishment.
That is, no off-path element is needed to establish the communication channel between the entity communicating the properies and the client.
1. Optionality.
The communication channel is strictly optional for the functioning of application flows.
A client's application flow must function even if the client does not establish the channel.
1. Scalability.
The mechanism must be scalable and implementable by Internet infrastructure as it exists today, for example mobile network packet cores.
1. Security.
The mechanism must ensure the confidentiality, integrity, and authenticity of the communication.
The mechanism must have independent security context from the application's security context.
The group must not define new security mechanisms for this purpose.
