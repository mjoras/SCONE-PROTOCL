The Secure Communication of Network Properties (SCONE-PRO) Working Group's primary objective is to define an on-path mechanism for securely communicating network properties to clients relevant to a given application, such as maximum achievable bandwidth for a video, specifically for QUIC connections carrying those applications.

The properies of this mechanism are as follows:

1. On-path establishment. That is, no off-path element is needed to establish the communication channel between the entity communicating the properies and the client.
2. Security. The mechanism must ensure the confidentiality, integrity, and authenticity of the communication. The mechanism must have independent security context from the application's security context. The group must not define new security mechanisms for this purpose.
3. Associativity with an application. The network properties must be associated with a given application traversing the network, for example a video playback.
4. Scalability. The mechanism must be scalable and implementable by Internet infrastructure as it exists today, for example mobile network packet cores.
