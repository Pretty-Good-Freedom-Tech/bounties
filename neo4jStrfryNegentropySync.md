Neo4Neg: neo4j strfry sync
=====

Goal of project: To design the strategy to synchronize a neo4j graph database with one (or more) strfry relays

This is a one-way sync. When activated, the service should ensure that for each event within the designated strfry relay matching the provided filter, there will be a corresponding node in neo4j of type: :NostrEvent associated with the corresponding event id. Additional node properties (e.g., author, created_at, etc) can be filled in later and do not necessarily need to be handled by the Neo4Neg service. 

## node types
- NostrUser
- NostrEvent
- NostrRelay
