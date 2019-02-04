# Segment-based recovery: Write-ahead logging revisited

This paper has one key idea - to relax the assumption that recovery grandularity is exactly a page. Instead, they advocate for the notion of segments that are separate from pages. This is in part motivated by the issues presented by multi-page records such as images. With segments that can span multiple files, the authors go further by eliminating the need for LSNs. This allows DMA to copy multiple pages at once.

Without LSNs, the database now cannot support arbitrary redo semantics. In fact, it only supports *blind writes*. These seem to be idempotent redo records that can be applied at-least-once which then relaxes the need for LSN. Why? The LSN is estimated (I was confued by this, however).

This structure also allows for on the fly re-ordering of transactions which allows for high-priority segments to get written to the log first. Also, the paper describes a way to combine ARIES with segments. The paper also presents a proof for correctness of ARIES and segment-based recovery. The analysis depends on examining the notion of "torn pages".

I liked this paper for how it was organized. It was extremely readable and explained the limitations of ARIES after many years. However, although it presents a simpler approach to recovery than ARIES, it mutes the impact by advocating for hybrid databases. Even with their proof of correctness, the complexity of this would be large. Ultimately, I like the ideas of restricting updates to idempotent transactions and then simplifying the interfaces between the app cache, buffer manager and log manager. But in the end, I think this paper had some shortcomings and I would not say it has had anywhere near the impact of the ARIES technique it tries to improve on.
