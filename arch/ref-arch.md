## Why SCONEPRO is needed
~~~~~~~~
                                            ----- 
                ------                     (     )              
               (      )    +---------+    (        )             
+--------+    ( Access )   | Traffic |   (    IP    )       +----------+
| Client +---( Network  )--+ Shaper  +--(   Network  )------+  Server  |
+--------+    (        )   +---------+   (          )       +----------+
               (-----)                    (       )         
                   Communication           (-----)           Content and 
                  Service Provider                       Application Provider
            |--------------------------|                    |------------|
~~~~~~~~
{: #withoutSP title="Video Traffic without SCONEPRO"}

Notes: 

* The client requests video content from a Content and Application Provider (CAP).
* The client provides application-level feedback to the CAP Server. (DASH, HLS, etc.)
   * The client is not aware of network conditions on the path toward the client.
   * This feedback is based on heuristics.
* The Communication Service Provider (CSP) attempts to detect and shape incoming video traffic, based on user data plans.
   * Detection and shaping are often based on heuristics, because the CSP isn't aware of the the details of the client's requests for video traffic from the CAP. 
   * As more and more Internet traffic becomes increasingly encrypted end-to-end, the CSP becomes increasingly unaware of these details, and increasingly reliant on heuristics. 
   * Traffic shaping based on heuristics is likely to be suboptimal, especially in cases where the client's access network is wireless, with its own rapid changes in available bandwidth.
* Because the CAP is aware that its traffic is being shaped in suboptimal ways, the CAP may design its own algorithms to detect and compensate for traffic shapers, but the CAP isn't aware of the details of the CSP's detection and traffic shaper deployment.
   * The combination of CSP traffic shaping and CAP responses to traffic shaping leads to unpredictable path behavior, and unpredictable path behavior confuses bandwidth estimation and congestion control procedures used for video delivery sessions. The end result is poor quality of experience for the end user. 
* As the CSP and CAP fumble in the dark to compensate for unpredictable responses from each other, they incur additional costs. For instance, the CSP must perform traffic detection and shaping for every flow, and this is compute-intensive. 

## One way SCONEPRO could work

This diagram omits a lot of detail, and there are other ways that SCONEPRO could work, but it's helpful to have a strawman for discussion.

~~~~~~~~
               +oooooooo+ 
  +------------> Client >---------------+
  |            o Opt-in o               |
  |            +ooo+oooo+               |  
  | (a)                                 |
  |           +ooovoooooo+              |
  |           o SCONEPRO o              |
  |   +-------< Guidance <-------+      |
  |   |       +oooooooooo+       |      |
  |   |                          | (b)  |        ----- 
  |   |          ------          |      |       (     )              
  |   |         (      )      +--+------v-+    (       )             
+-+---v--+     ( Access )     | SCONEPRO  |   (    IP   )       +----------+
| Client +====( Network  )====+ Monitor   +==(  Network  )======+  Server  |
+--------+     (        )     +-----------+   (         )       +----------+
                (------)                       (       )         
                   Communication                (-----)          Content and 
                  Service Provider                          Application Provider
             |-----------------------------|                   |-------------|
~~~~~~~~
{: #withSP title="Video Traffic with SCONEPRO"}

This example assumes a model where the client performs self-adaptation based on adaptation parameters provided by the CSP, that do not attempt to take advantage of client-specific capabilities. 

Notes: 

* (a) The client opts in to the Communication Service Provider (CSP) SCONEPRO Service.
* (b) The CSP creates an initial SCONEPRO adaptation guidance control block for the client, and provides initial adaptation guidance for the client. 
* The client requests video content from a Content and Application Provider (CAP).
* The client takes the adaptation guidance it has received into account when providing feedback to the CAP Server.
* The CSP's SCONEPRO Monitor observes whether the client's incoming packet stream conforms to the adapation guidance provided to the client.
   * If the incoming packet stream conforms to that guidance, the SCONEPRO Monitor takes no action.
   * If the incoming packet stream does not conform to that guidance, the SCONEPRO Monitor takes action as it would for any other packet stream.
* The SCONEPRO Monitor doesn't need to detect video flows from a client using the SCONEPRO Service. It only needs to recognize that a client using the SCONEPRO service isn't self-adapting based on the SCONEPRO adaptation guidance.

Spencer's opinion is that including client-specific capabilities might improve the client experience in the short term, but minimizing the CSP's knowledge of client capabilities and relying on the client to conform to generic SCONEPRO guidance will make SCONEPRO less likely to ossify, since client adaptation behavior can change without requiring corresponding changes at the CSP.
 