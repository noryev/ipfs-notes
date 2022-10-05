Reasons for limitation:

security - easy to DOS nodes without forcing small chunks
deduplication - small chunks can dedup. big ones effectively dont.
latency - can externalize small pieces already (think a stream)
bandwidth - optimize the use of bandwidth across many peers
performance - much better perf to hold small pieces in memory. hash along the dag to verify the whole thing.
the big DOS problem with huge leaves is that malicious nodes can serve bogus stuff for a long time before a node can detect the problem (imagine having to download 4GB before you can check whether any of it is valid). this was super harmful for bittorrent (when people started choosing huge piece sizes), attackers would routinely do this, very cheaply-- just serve bogus random data. smaller chunks are very important here.

the way i would approach what you describe (which is pretty cool) is that canonical should both:

provide the leaf hash with CIDv1. ipfs could address it but not easily transfer it (there may be exceptions here, where it could be a tunable parameter).
provide a new graph (chunked, dedup, etc), whose output matches the other leaf.
that way ipfs could pull the chunked one, and verify the whole one afterwards.
you raise a good point though that we need to address how to look at objects and know whether to pull them when they may be too big.
