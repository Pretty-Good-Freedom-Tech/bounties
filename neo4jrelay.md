neo4jrelay: synchronization of neo4j relay with nostr
=====
alternate name: neostrfry, the strfry to neo4j ETL pipeline
-----

[Nostr](https://nostr.com/) is an open source protocol for decentralized of social media endorsed by Jack Dorsey which boasts hundreds of independent apps and app developers and 20,000 average daily users. 

Graph databases such as [neo4j](https://neo4j.com/) and the decentralized web of trust that many are tying to build with nostr are a match made in heaven. Regrettably, only a small handful of nostr developers are familiar with graph databases in general or neo4j in particular. The goal of this project is to make neo4j more accessible to a wide range of nostr developers by the creation of a nostr relay powered by neo4j.

Specifically, the goal of this project is to design and implement a set of open source tools which together comprise an ETL pipeline from a nostr relay to a neo4j database. The relay of choice is [strfry](https://github.com/hoytech/strfry), although other relays could be considered.

The initial application of these tools is a personal web of trust relay. Centrality algos such as personalized pageRank will be used to regulate which data is kept and which is discarded. Ideally, these tools will be ported over to [relay tools](https://github.com/relaytools), which is a fork of strfry.

The secondary application is an enterprise nostr search engine, a google search for nostr, which will be an expansive cache of all nostr events. Like nostr.band but with neo4j. The volume of data will be large: currently half a billion events, with 1 million new events per day, according to [stats.nostr.band](https://stats.nostr.band).

#### Step 1: planning

Generation of a report with an outline of the overall strategy to achieve **core goals** as well as the a**dvanced goals** as described below
- what is the best import strategy for initialization of a new db or import into the db of a very large data volume, e.g. nostrhole (see below)? Up to 1 billion events
- what is the best import strategy for real-time import of data as new events are received by the relay? Assume data pipeline rates up to 10 million events per day but use different techniques for different rates. Personal WoT relays will have much lower rates: on the order of one per second 
- what is the best method to load events that may have been missed? Optimal time interval to run such a script?
- detailed strategy for each major import tool: data importer, cypher: load csv, APOC, neo4j-admin
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

There are many relay implementations. Strfry is my top choice for several reasons. 
- widely recognized as the fastest relay
- LMDB
- the basis of relay-tools

Second choice might be nostrDB. However, it's in heavy development mode.

An attractive option would be to sync to LMDB in a way that is independent of strfry. This could be readily ported to any relay which uses or supports LMDB, which includes strfry, khatru, and nostrDB. Although of note, strfry actually uses a fork of LMDB.

#### relay options

[strfry](https://github.com/hoytech/strfry). Many projects such as relay-tools are derived from strfry.

[khatru](https://github.com/fiatjaf/khatru)

[nostream](https://github.com/Cameri/nostream): typescript, PostgreSQL.

[nostrDB](https://github.com/damus-io/nostrdb) - not a relay, but a database; "an unfairly fast embedded nostr database backed by lmdb." "This entire design of nostrdb is copied almost entirely from strfry, the fastest nostr relay. The difference is that nostrdb is meant to be embeddable as a C library into any application with full nostr query support."

Many nostr relays use LMDB. One potential strategy would be to design this as an LMDB-to-neo4j ETL pipeline which could then be implemented using other relays including notedeck's nostrDb.

For a comprehensive list see the relay section of [awesome nostr](https://github.com/aljazceru/awesome-nostr).

## data

[nostr](https://nostr.com/) currently boasts 20k daily active users, as reported by [nostr.band](https://stats.nostr.band)

#### resources with raw data

Not including relays, large data repositories include nostr.band and primal.net.

[nostrhole data](https://archive.v0l.io/); see [this post](https://njump.me/nevent1qqswv9q0766ymzttdf46fzpwdny0wy2rrgjyffz05zqdh3djz3rl8dgprpmhxue69uhhqunfd46hxtnwdaehgu339e3k7mf0qgsx8lnrrrw9skpulctgzruxm5y7rzlaw64tcf9qpqww9pt0xvzsfmgrqsqqqqqphnqgs8)

[nostrDB testdata, profiles](http://git.jb55.com/nostrdb/file/testdata/profiles.json.html)

## data model 

### neo4j node labels

- NostrUser; properties: pubkey, personalizedPageRank
- NostrEvent; properties: eventId, kind, created_at, author, replaceable (boolean)
- NostrRelay; properties: url

### neo4j edge types

NostrUser to NostrUser
- FOLLOW; see [NIP-02](https://github.com/nostr-protocol/nips/blob/master/02.md); properties: eventId, created_at, which are the event id and its timestamp of the kind 3 event which added this follow
- MUTE; see kind 10000 events described in [NIP-51](https://github.com/nostr-protocol/nips/blob/master/51.md); properties: eventId, created_at, which are the event id and its timestamp of the kind 10000 event which added this follow
- REPORT; see [NIP-56](https://github.com/nostr-protocol/nips/blob/master/56.md); properties: reportType (spam, nudity, etc); eventId

NostrUser to NostrEvent
- author (IS_THE_AUTHOR_OF)
- PROFILE

NostrEvent to NostrEvent
- REACTION; see [NIP-25](https://github.com/nostr-protocol/nips/blob/master/25.md)
- REPLY; see [NIP-10](https://github.com/nostr-protocol/nips/blob/master/10.md)

#### class threads

Link to description of class threads.

### Concept Graph Node Types:
- Word;
- Set; properties: 

Initialize node:Set for each supported event kind: 

### Concept Graph Edge Types:
- threadInitiation 
- threadProgagation SUBSET_OF
- threadTermination SPECIFIC_INSTANCE_OF


## Progress

strfry and neo4j on the same relay 

modification of the strfry export command to generate csv

## Open questions

Should strfry and neo4j be on the same server versus different servers?

rationale for messageBroker like RabbitMQ?

#### replaceable versus irreplaceable events

How to deal with replaceable versus irreplaceable events. Two different node types? delete events once replaced?

## Related projects 

[neostr](https://github.com/wisehodl/neostr), a neo4j graph-native eventstore for nostr. Similar goals of the current project, except focus is more on calculation of WoT scores and less focus on the ETL pipeline itself. 
