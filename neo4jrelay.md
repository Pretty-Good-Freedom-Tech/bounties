neo4jrelay: synchronization of neo4j relay with nostr
=====
alternate name: neostrfry, the strfry to neo4j ETL pipeline
-----

[Nostr](https://nostr.com/) is an open source protocol for decentralized of social media endorsed by Jack Dorsey which boasts hundreds of independent apps and app developers and 20,000 average daily users. 

Graph databases such as [neo4j](https://neo4j.com/) and the decentralized web of trust that many are tying to build with nostr are a match made in heaven. Regrettably, only a small handful of nostr developers are familiar with graph databases in general or neo4j in particular. The goal of this project is to make neo4j more accessible to a wide range of nostr developers by the creation of a nostr relay powered by neo4j.

Specifically, the goal of this project is to design and implement a set of open source tools which together comprise an ETL pipeline from a nostr relay to a neo4j database. The relay of choice is [strfry](https://github.com/hoytech/strfry), although other relays could be considered.

The initial application of these tools is a personal web of trust relay. Centrality algos such as personalized pageRank will be used to regulate which data is kept and which is discarded. Ideally, these tools will be ported over to [relay tools](https://github.com/relaytools), which is a fork of strfry.

The secondary application is an enterprise nostr search engine, a google search for nostr, which will be an expansive cache of all nostr events. Like nostr.band but with neo4j. The volume of data will be large: currently half a billion events, with 1 million new events per day, according to [stats.nostr.band](https://stats.nostr.band).

#### Step 1: initial exploration

Generation of a report with an outline of the overall strategy to achieve **core goals** as well as the a**dvanced goals** as described below
- which import tools to use (data importer, cypher: load csv, APOC, neo4j-admin)
- estimations of costs and length of time to complete goals

#### core goals

Completion would include generation of code, open sourced under PGFT, and would include documentation for nostr developers and advanced users to set up their own neo4j server (AWS or other), and should include testing by perhaps a handful of nostr devs and users.

#### Advanced goals

would include scripts to manage knowledge graph, including update class threads
calculation of personalized pageRank
tools to manage strfry filters and plugins 

Applications of this tool will fall on two ends of the spectrum depending on how much data they expect to handle. Nearly half a billion nostr events (notes) have been generated so for on nostr, with roughly one million new notes per day. I currently envision two use cases:
- Global nostr cache: an enterprise that seeks to store every nostr event it comes across and make it searchable. Think: nostr.band augmented by neo4j for more complex and performant search queries
- Personal Web of Trust relay: Think: relay.tools augmented by neo4j for calculation of web of trust scores

## choice of relay 

There are many relay implementations. 

[strfry](https://github.com/hoytech/strfry). Many projects such as relay-tools are derived from strfry.

[khatru](https://github.com/fiatjaf/khatru)

[nostream](https://github.com/Cameri/nostream): typescript, postgresql.

Many nostr relays use LMDB. One potential strategy would be to design this as an LMDB-to-neo4j ETL pipeline which could then be implemented using other relays including notedeck's nostrDb.

For a comprehensive list see the relay section of [awesome nostr](https://github.com/aljazceru/awesome-nostr).

## data

[nostr](https://nostr.com/) currently boasts 20k daily active users, as reported by [nostr.band](https://stats.nostr.band)

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

[neostr](https://github.com/wisehodl/neostr), a neo4j graph-native eventstore for nostr. Similar goals of the current project, except focus is more on calculation of WoT scores and less focus on the ETL pipeline itself. 
