synchronization of neo4j with nostr
=====
strfry to neo4j ETL pipeline
-----

The goal of this project is to design and implement a set of open source tools which together comprise an ETL pipeline from nostr to a neo4j database. Long term vsion would include applications (individual, community edition) as well as enterprise-level applications.

#### Step 1

an outline of the overall strategy to achieve core goals, such as which import tools to use (data importer, cypher: load csv, APOC, neo4j-admin)

#### core goals

Completion would include generation of code, open sourced under PGFT, and would include documentation for nostr developers and advanced users to set up their own neo4j server (AWS or other), and should include testing by perhaps a handful of nostr devs and users.

#### Advanced goals

would include scripts to manage knowledge graph, including update class threads
calculation of personalized pageRank
tools to manage strfry filters and plugins 

Applications of this tool will fall on two ends of the spectrum depending on how much data they expect to handle. Nearly half a billion nostr events (notes) have been generated so for on nostr, with roughly one million new notes per day. I currently envision two use cases:
- Global nostr cache: an enterprise that seeks to store every nostr event it comes across and make it searchable. Think: nostr.band augmented by neo4j for more complex and performant search queries
- Personal Web of Trust relay: Think: relay.tools augmented by neo4j for calculation of web of trust scores

## Background

[nostr](https://nostr.com/) is an open source protocol to build decentralized platforms. It currently boasts 20k daily active users, as reported by [nostr.band](https://stats.nostr.band)

## relays 

Strfry. Many projects such as relay-tools are derived from strfry.

Many nostr relays use LMDB. One potential strategy would be to design this as an LMDB-to-neo4j ETL pipeline which could then be implemented using other relays including notedeck's nostrDb.

## data

#### resources with raw data

Not including relays, large data repositories include nostr.band and primal.net.

[nostrhole data](https://archive.v0l.io/); see [this post](https://njump.me/nevent1qqswv9q0766ymzttdf46fzpwdny0wy2rrgjyffz05zqdh3djz3rl8dgprpmhxue69uhhqunfd46hxtnwdaehgu339e3k7mf0qgsx8lnrrrw9skpulctgzruxm5y7rzlaw64tcf9qpqww9pt0xvzsfmgrqsqqqqqphnqgs8)

## neo4j node types

- NostrUser
- NostrEvent, properties: kind, created_at, replaceable
- NostrRelay

## neo4j edge types

NostrUser to NostrUser
- follows (FOLLOW)
- mutes (MUTE)
- reports (REPORT) - should include report type

NostrUser to NostrEvent
- author (IS_THE_AUTHOR_OF)

NostrUser to replaceable NostrEvent
- author (IS_THE_AUTHOR_OF)

#### class threads

Link to description of class threads.

## Progress

strfry and neo4j on the same relay 

modification of the strfry export command to generate csv

## Open questions

Should strfry and neo4j be on the same server versus different servers?

#### replaceable versus irreplaceable events

How to deal with replaceable versus irreplaceable events. Two different node types? delete events once replaced?

## Related projects 

[neostr](https://github.com/wisehodl/neostr)
