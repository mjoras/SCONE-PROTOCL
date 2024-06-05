# Name: Securely COmmunicating NEtwork PROperties SCONEPRO
## Description
Video traffic is 70% of the overall traffic volume on the Internet and is expected to grow to 80% by 2028. Across developed and emerging markets video traffic forms 50-80% of traffic volume on mobile networks. New formats like short form videos have seen tremendous growth in recent years. These growth trends are likely to increase with new populations coming online on mobile-first markets.

Local mobile radio conditions may constrain the maximum throughput for a given client, or be so volatile as to rapidly change the maximum throughput throughout the course of a session. In addition, despite capacity augmentation work such as deployment of new generations or new bands of spectrum, capacity augmentation efforts are not keeping pace with growth in demand. These network operators have found it faster and less expensive to invest in shaping (also called throttling) of video traffic on a per-flow basis, which negatively affects video stream quality. This is done for both network management and business motivations. Network operators cannot explicitly measure the degradation to end user quality of experience (QoE) caused by traffic shaping, making this approach open loop.

Video traffic usually employs adaptive bitrate (ABR) schemes to dynamically adjust the video quality (and thus the data rate) in response to changing network conditions. Ideally, when a network operator performs traffic shaping, the ABR scheme should adapt the video quality in use to reflect the data rate allowed by shaping, and converge on a bitrate allowed by the shaper. In practice this convergence is extremely difficult to achieve while maintaining a good user experience. Application providers are even designing algorithms to detect the presence of such traffic shapers and estimate the targeted shaping rate, however, these algorithms are likely to be both inaccurate and complex. Instead, it would be beneficial, for both the application provider and network operator, to signal network attributes to the application to self-adapt its video traffic to conform to the specified characteristics. The application provider has the ability to measure end user QoE and therefore can self-adapt with QoE feedback.

## Required Details
- Status: WG Forming
- Responsible AD: Zahed Sarker
- BOF proponents: Matt Joras <matt.joras@gmail.com>, Marcus Ihlar <marcus.ihlar@ericsson.com>, Spencer Dawkins <spencerdawkins.ietf@gmail.com>
- Number of people expected to attend: 100
- Length of session (1 or 2 hours): 2 hours
- Conflicts (whole Areas and/or WGs)
   - Chair Conflicts: TBD
   - Technology Overlap: quic, tsvwg, ccwg, masque, iccrg, moq, mops, webtrans, avtcore, httpbis
   - Key Participant Conflict: quic, tsvwg, moq, ippm, avtcore

## Information for IAB/IESG

The proponents believe that a new working group is required. This is a follow up on a non WG forming BOF at IETF 119. The outcome of that meeting was questions that the chairs and proponents believed needed to be answered before forming a WG. Since then work has been done on GitHub ( see issues here: https://github.com/mjoras/SCONE-PROTOCL tagged as RaisedAt119) and through Internet Drafts (see below) to answer some of those questions.

## Agenda
- Will be formulated with chairs.
- Focus on review of work since IETF 119 and the working charter, with discussion and AD questions.

## Links to the mailing list, draft charter if any, relevant Internet-Drafts, etc.
   - Mailing List: https://www.ietf.org/mailman/listinfo/sadcdn
   - Draft charter: https://github.com/mjoras/SCONE-PROTOCL/blob/main/documents/charter.md
   - Relevant Internet-Drafts:
  	- https://datatracker.ietf.org/doc/draft-joras-sconepro-video-opt-requirements/
  	- https://datatracker.ietf.org/doc/draft-tomar-sconepro-privacy/
  	- https://datatracker.ietf.org/doc/draft-eddy-sconepro-api/
  	- https://datatracker.ietf.org/doc/draft-tan-sconepro-netneutrality/
