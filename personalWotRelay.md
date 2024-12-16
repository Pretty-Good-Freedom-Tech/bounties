Personal Nostr Web of Trust Relay
=====

## Goal of the project: 

construction of a FOSS nostr relay that 

Similar to utxo's personal web of trust relay, but with more advanced methods of defining web of trust. utxo's defines WoT as follows of my follows. (is this correct ????)

## Details

- use either strfry OR fiatjaf's nostr relay
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