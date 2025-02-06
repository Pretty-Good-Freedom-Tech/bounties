synchronization of neo4j with nostr
=====
strfry to neo4j ETL pipeline
-----

The goal of this project is to design and implement a set of open source tools which together comprise an ETL pipeline from nostr to a neo4j database. 

Applications of this tool will fall on two ends of the spectrum depending on how much data they expect to handle. Nearly half a billion nostr events (notes) have been generated so for on nostr, with roughly one million new notes per day. I currently envision two use cases:
- Global nostr cache: an enterprise that seeks to store every nostr event it comes across and make it searchable. Think: nostr.band augmented by neo4j for more complex and performant search queries
- Personal Web of Trust relay: Think: relay.tools augmented by neo4j for calculation of web of trust scores

## Background

[nostr](https://nostr.com/) is an open source protocol to build decentralized platforms. It currently boasts 20k daily active users, as reported by [nostr.band](https://stats.nostr.band)

## relays 

Strfry. Many projects such as relay-tools are derived from strfry.

Many nostr relays use LMDB. One potential strategy would be to design this as an LMDB-to-neo4j ETL pipeline which could then be implemented using other relays including notedeck's nostrDb.

## 4 ways to load data into neo4j; progress on each area

1. csv

## neo4j node types

- NostrUser
- NostrEvent
- NostrRelay

## neo4j edge types

NostrUser to NostrUser
- follows
- mutes
- reports

NostrUser to NostrEvent

## replaceable versus irreplaceable events

## Open questions

Should strfry and neo4j be on the same server versus different servers?

