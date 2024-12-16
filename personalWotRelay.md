Graph-Database-powered Personal Nostr Web of Trust Relay
=====

## Goal of the project: 

construction of a FOSS nostr relay that calculates and keeps track of the relay owner's web of trust, using graph database centrality algorithms (including but not limited to PageRank) to define the web

Similar to utxo's personal web of trust relay (see refs below), but with more advanced methods of defining web of trust.

## Details

- use either strfry OR fiatjaf's nostr relay khatru
- neo4j for graph database, although will consider other open source graph database implementations
- ability to calculate pagerank scores of everyone in your network
- Your WoT is defined as every pubkey with pagerank score above an arbitrarily chosen threshold

Minimum product will have the following features:
- local storage of all kind 3 notes
- continuous update of pagerank scores using FOLLOWS

More advanced will allow:
- selection of note kinds which will be stored for all npubs in the WoT, e.g. all kind 1 notes authored by anyone with pagerank score above threshold

## Purposes

The long term goal will be to move beyond pagerank and experiment with different centrality algorithms, possibly using multiple algos to keep trakc of multiple webs of trust, using data not limited to follows.

## References

- [utxo's WoT relay](https://github.com/bitvora/wot-relay), which uses "follows of my follows" as web of trust
- [HAVEN](https://github.com/bitvora/haven) (not sure how it calculates WoT)
- [Sep 2024 thread with list of WoT relays](https://nostr.cxplay.org/nevent1qqszl5x33zks8k2wh2eh6c7kncphjsngc0kz4ktfueje9drm3d47wxgpz4mhxue69uhkummnw3ezummcw3ezuer9wchsygplwuxkt5a8vj5utj6s8tsj8e3wcavc45p4mqmw92qs7wrh5azmyspsgqqqqqqsxa6gcy)
- [khatru](https://github.com/fiatjaf/khatru) - framework for custom relays, by fiatjaf; see also [this link](https://khatru.nostr.technology/)
- [strfry](https://github.com/hoytech/strfry)
