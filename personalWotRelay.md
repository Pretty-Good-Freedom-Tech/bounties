Graph Database powered Personal Nostr Web of Trust Relay
=====
using neo4j or other FOSS graph database
-----

## Overview: 

construction of a FOSS nostr relay that calculates and keeps track of the relay owner's web of trust (WoT), defined using graph database centrality algorithms, starting with PageRank but with the intention to explore other options

ideally, neo4j as the graph database and neo4j Graph Data Science library for PageRank and other centrality algorithms, but alternate tools will be considered as long as they're FOSS

## Background and motivation

Existing nostr WoT relays define WoT using relatively crude methods. Utxo's WoT relay, for example, defines a user's WoT very simply, as my follows + the follows of my follows. While useful, this approach suffers from a number of shortcomings, including uncertainties over how to contextualize trust, how to incorporate data beyond simple follows, and how to personalize individual preferences, beliefs and values. We believe that graph databases offer much more sophisticated, powerful, and flexible algorithms that have the potential to address each of these shortcomings. Fortunately, sophisticated FOSS tools such as neo4j, cypher, and the neo4j Graph Data Science library exist that are well suited to this purpose.

## Desired features

- start with either strfry OR fiatjaf's nostr relay khatru
- incorporate neo4j graph database, although will consider other open source graph database implementations
- keep track of the reference user's Follows Network: all pubkeys connected to the reference user, using kind 3 follows, with no limit to the number of hops away (expected to be between 150k-200k npubs, as of Dec 2024)
- keep an up to date neo4j graph: users as nodes, follows as edges
- incorporate the neo4j Graph Data Science library and use it to calculate and keep up to date PageRank
- update the Follows Network and pagerank scores continuously or with high frequency
- The reference user's baseline WoT will be defined as every pubkey with pagerank score above an arbitrarily chosen threshold

## Utility

More advanced versions of this project will allow:
- abiilty to adjust the threshold pagerank score for inclusion in the baseline WoT
- selection of note kinds which will be stored for all pubkeys in the WoT, e.g. the option to store all kind 1 notes authored by anyone with pagerank score above threshold

The long term goal will be to move beyond pagerank and experiment with different centrality algorithms, possibly using multiple algos to keep track of multiple webs of trust, using data not limited to follows. 

A chief candidate for next-gen centralizty algo will be the GrapeRank algorithm.
- incorporates follows, mutes and reports (NIP-56, kind 1984) to define the baseline web of trust
- defines a pathway for incorporation of new sources of data (e.g. NIP 32 labels, zaps, reactions, replies, etc)
- multiple webs of trust, each one corresponding to a distinct context
- customizable to individual user preferences and values

## candidates

This is a work in progress -- but if you're interested, send me a DM at: npub1u5njm6g5h5cpw4wy8xugu62e5s7f6fnysv0sj0z3a8rengt2zqhsxrldq3 

Ideal candidates will have expertise in the following areas:
- neo4j, cypher, neo4j Graph Data Science, and centrality algorithms
- nostr relay management

## References

- [utxo's WoT relay](https://github.com/bitvora/wot-relay), which uses "follows of my follows" as web of trust
- [HAVEN](https://github.com/bitvora/haven) (not sure how it calculates WoT)
- [Sep 2024 thread with list of WoT relays](https://nostr.cxplay.org/nevent1qqszl5x33zks8k2wh2eh6c7kncphjsngc0kz4ktfueje9drm3d47wxgpz4mhxue69uhkummnw3ezummcw3ezuer9wchsygplwuxkt5a8vj5utj6s8tsj8e3wcavc45p4mqmw92qs7wrh5azmyspsgqqqqqqsxa6gcy)
- [khatru](https://github.com/fiatjaf/khatru) - framework for custom relays, by fiatjaf; see also [this link](https://khatru.nostr.technology/)
- [strfry](https://github.com/hoytech/strfry)
