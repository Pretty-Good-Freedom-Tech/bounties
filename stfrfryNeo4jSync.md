synchronization of neo4j with nostr
=====

The goal of this project is to design and implement a set of open source tools which together comprise an ETL pipeline from nostr to a neo4j database. 

Applications of this tool will fall on two ends of the spectrum depending on how much data they expect to handle. Nearly half a billion nostr events (notes) have been generated so for on nostr, with roughly one million new notes per day. I currently envision two use cases:
- Global nostr cache: an enterprise that seeks to store every nostr event it comes across and make it searchable. Think: nostr.band augmented by neo4j for more complex and performant search queries
- Personal Web of Trust relay: Think: relay.tools augmented by neo4j for calculation of web of trust scores

## Background

[nostr](https://nostr.com/) is an open source protocol to build decentralized platforms. It currently boasts 20k daily active users.

## Where does nostr data come from?

nostr 

## 4 ways to load data into neo4j

