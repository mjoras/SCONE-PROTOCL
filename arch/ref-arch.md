## Why SCONEPRO is needed
~~~~~~~~
                                            ----- 
                ------                     (     )              
               (      )    +---------+    (        )             
+--------+    ( Access )   | Traffic |   (    IP    )       +----------+
| Client +---( Network  )--+ Shaper  +--(   Network  )------+  Server  |
+--------+    (        )   +---------+   (          )       +----------+
               (-----)                    (       )         
                                           (-----)           Content and 
   Communication Service Provider                       Application Provider
 |------------------------------------|                    |------------|
~~~~~~~~
{: #withoutSP title="Video Traffic without SCONEPRO"}

Notes: 

* The client requests video content from a Content and Application Provider (CAP).
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
              +--------+ 
  +---------> | Client |
  |           | Opt-in |
  |           +---+----+                
  | (a)           |  (b)
  |           +---v-----+ 
  |           | Shaping |
  |   +-------+ Guidance| <------+
  |   |       +---------+        |
  |   |                          | (c)        ----- 
  |   | (d)      ------          |           (     )              
  |   |         (      )     +---+-----+    (        )             
+-+---v--+     ( Access )    | Traffic |   (    IP    )       +----------+
| Client +----( Network  )---+ Shaper  +--(   Network  )------+  Server  |
+--------+     (        )    +---------+   (          )       +----------+
                (------)                    (        )         
                                             (-----)           Content and 
   Communication Service Provider                          Application Provider
 |---------------------------------------|                   |------------|
~~~~~~~~
{: #withSP title="Video Traffic with SCONEPRO"}

Notes: 

* (a) The client opts in to the Communication Service Provider (CSP) SCONEPRO Service
* (b) The CSP creates a shaping guidance control block for the client
* The client requests video content from a Content and Application Provider (CAP).
* (c) The CSP's traffic shaper provides shaping guidance for the client 
* (d) The client takes this shaping guidance into account when providing application-level feedback to the CAP Server
* The CSP's traffic shaper observes whether the incoming packet stream conforms to the shaping guidance provided to the client.
   * If the incoming packet stream conforms to that guidance, the traffic shaper takes no action
   * If the incoming packet stream does not conform to that guidance, traffic shaping takes place as it would for any other packet stream.
 