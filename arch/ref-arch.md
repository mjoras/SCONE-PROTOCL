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
                      Communication                             Content and 
                     Service Provider                       Aplication Provider
             |--------------------------------|           |---------------------|
~~~~~~~~
{: #SParch title="SCONEPRO Reference Architecture"}

SCONEPRO assumes a network architecture with three components:

* A Client that consumes a video stream, and is capable of opting into a Communication Service Provider's SCONEPRO service 
* A Server that produces a video stream
* A SCONEPRO Monitor, located on the path between the Client and the Server, that is capable of providing network properties to a Client that opts in to the Communication Service Provider's SCONEPRO service

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
                      Communication                             Content and 
                     Service Provider                       Aplication Provider
             |--------------------------------|           |---------------------|
~~~~~~~~
{: #withSP title="Video Traffic with SCONEPRO"}

This example assumes a model where the client performs self-adaptation based on adaptation parameters provided by the CSP, that do not attempt to take advantage of client-specific capabilities. 

Notes: 

* (a) The client opts in to the Communication Service Provider's (CSP) SCONEPRO Service.
* (b) The CSP creates an initial SCONEPRO adaptation properties control block for the client, and provides initial adaptation properties for the client. 
* The client requests video content from a Content and Application Provider (CAP).
* The client takes the adaptation properties it has received into account when providing feedback to the CAP Server.
* The CSP's SCONEPRO Monitor observes whether the client's incoming packet stream conforms to the adaptation properties provided to the client.
   * If the incoming packet stream conforms to those properties, the SCONEPRO Monitor takes no action.
   * If the incoming packet stream does not conform to those properties, the SCONEPRO Monitor takes action as it would for any other packet stream.
* (b) If the path characteristics between the Server and Client change, the CSP's SCONEPRO Monitor sends updated adaptation properties to the client.
* The SCONEPRO Monitor doesn't need to detect video flows from a client using the SCONEPRO Service. It only needs to recognize that a client using the SCONEPRO service isn't self-adapting based on the SCONEPRO adaptation properties.

Spencer's opinion is that including client-specific capabilities might improve the client experience in the short term, but minimizing the CSP's knowledge of client capabilities and relying on the client to conform to generic SCONEPRO properties will make SCONEPRO less likely to ossify, since client adaptation behavior can change without requiring corresponding changes at the CSP.
