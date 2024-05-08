## SCONEPRO Reference Architecture

This diagram omits a lot of detail, and there are other ways that SCONEPRO could work, but it's helpful to have a strawman for discussion.

~~~~~~~~

                                                  ----- 
                 ------                          (     )              
                (      )      +--^------v-+     (       )             
+-^---v--+     ( Access )     | SCONEPRO  |    (    IP   )       +----------+
| Client +====( Network  )====+  Monitor  +===(  Network  )======+  Server  |
+--------+     (        )     +-----------+    (         )       +----------+
                (------)                        (       )         
                                                 (-----)
              Communication                                      Content and 
            Service Provider                                 Aplication Provider
 |-----------------------------------------------|     |--------------------------|
~~~~~~~~
{: #SParch title="SCONEPRO Reference Architecture"}

SCONEPRO assumes a network architecture with these components:

* A Client that 
    * consumes at least one Adaptive Bit Rate (ABR) video stream, 
    * is connected to a network provided by a Communication Service Provider (CSP), and
    * is capable of opting into a CSPs's SCONEPRO service 
* A SCONEPRO Monitor that 
    * is capable of providing network properties to a Client, 
    * is also connected to a network provided by the same CSP and 
    * is located on the path between the Client and the Server
* A Server that 
    * produces at least one ABR video stream, and
    * is connected to a network provided by a Content and Application Provider (CAP)

Notes: 

## One Way SCONEPRO Could Work

~~~~~~~~
               +oooooooo+ 
  >------------> Client >---------------v
  |            o Opt-in o               |
  |            +ooo+oooo+               |  
  | (a)                                 |
  |          +ooovooooooo+              |
  |          o  SCONEPRO o              |
  |   v------< Properties<-------<      |
  |   |      +ooooooooooo+       |      |
  |   |                      (b) |      |         ----- 
  |   |          ------          |      |        (     )              
  |   |         (      )      +--^------v-+     (       )             
+-^---v--+     ( Access )     | SCONEPRO  |    (    IP   )       +----------+
| Client +====( Network  )====+  Monitor  +===(  Network  )======+  Server  |
+--------+     (        )     +-----------+    (         )       +----------+
                (------)                        (       )         
                                                 (-----)
              Communication                                      Content and 
            Service Provider                                 Aplication Provider
 |-----------------------------------------------|     |--------------------------|
~~~~~~~~
{: #withSP title="Video Traffic with SCONEPRO"}

* (a) The Client opts in to the Communication Service Provider's (CSP) SCONEPRO Service
* (b) The CSP creates an initial SCONEPRO adaptation properties control block for the Client, and provides initial adaptation properties for the Client
* The Client takes the adaptation properties it has received from the SCONEPRO Monitor into account when requesting ABR video from the Server
* The Client requests ABR video content from a Server
* The Server provides the requested ABR video content to the Client
* The CSP's SCONEPRO Monitor observes whether the Client's incoming packet stream conforms to the adaptation properties provided to the Client
   * If the incoming packet stream conforms to those properties, the SCONEPRO Monitor takes no action
   * If the incoming packet stream does not conform to those properties, the SCONEPRO Monitor takes action as it would for any other packet stream
* (b) If the path characteristics between the Server and Client change, the CSP's SCONEPRO Monitor might send updated adaptation properties to the Client

Notes: 

SCONEPRO adapation properties will often reflect a business relationship between the Client and the CSP, but this isn't necessary, and might also reflect changing network conditions within CSP's network.

(Is this true?) The CSP and CAP may also have a business relationship that includes traffic parameters, but the chartered goals for SCONEPRO don't target the network path between the CSP and the CAP

The SCONEPRO Monitor doesn't need to detect video flows from a Client using the SCONEPRO Service. It can recognize the situation where a Client using the SCONEPRO service isn't self-adapting based on the SCONEPRO adaptation properties. What the CSP does in response is outside the scope of SCONEPRO

This example assumes a model where the Client performs self-adaptation based on adaptation parameters provided by the CSP, that do not attempt to take advantage of Client-specific capabilities. Including Client-specific capabilities might improve the Client experience in the short term, but minimizing the CSP's knowledge of Client capabilities and relying on the Client to conform to generic SCONEPRO properties will make SCONEPRO less likely to ossify, since Client adaptation behavior can change without requiring corresponding changes at the CSP.
