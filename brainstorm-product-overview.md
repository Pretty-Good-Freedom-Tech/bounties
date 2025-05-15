Product name: Grapevine 
=====
(alt product name: Brainstorm)
-----

# Product Overview

## One-line pitches:
- to prospective neo4j engineers: a neo4j nostr relay
- to the purple pilled: a personalized WoT nostr relay
- to Randy: a personalized knowledge graph that your community helps you to manage

## one-paragraph pitch:
The Grapevine is a personalized nostr relay that uses your community -- what nostr users call your web of trust -- to identify who is the most trustworthy to curate content, facts, and information for you, in any given context. The Grapevine harnesses neo4j in two ways: first, to organize nostr notes into a knowledge graph; and second, to calculate importance scores using the kinds of algorithms that can only be done at scale using a graph database. 

Nostr and neo4j are a match made in heaven. This is the missing ingredient for nostr to go mainstream. Millions of users, every one of whom will want their own Grapevine. Every development team is sleeping on this. The time to strike is now.

## Target customers
1. Personalized datastore for the average consumer. TAM: 8 billion.
2. Enterprise. TAM: every company that has a website will want a Grapevine.

## Tech stack
1. Nostr relay
2. Graph database

## Questions: tech stack
1. Which nostr relay? strfry, khatru are leading options.
2. Should the nostr relay and graph db be on the same instance?
3. Maximum possible throughput. 
4. hardware requirements and costs per customer

## Product development

Goal will be to validate the product and to answer the above tech stack questions, determine costs, flesh out a business plan.

Engage neo4j experts to create neo4j nostr relay and answer the above questions for each of these versions:

- v0.1 neo4j only. kind 1 only. node types: NostrUsers. Relationship type: FOLLOWS. relay connection will be by websocket. Calculates PageRank, dos, verified follows.
- v0.2. kinds 3, 1000. Follows, Mutes, Reports. Calculates GrapeRank.
- v1.0. all desired event kinds, organized into a mature Knowledge Graph

Each version will be neo4j only and will connect to relay via websocket. Relay will be added to instance if/when necessary to achieve faster data synchronization.

## Data throughput

Statistics reflect current usage. Feasibilty studies should anticipate increases by up to 5 orders of magnitude.

average daily users: 15k-20k
average daily notes by kind

## Product rollout

1. Brainstorm Relays
- series of branded strfry relays
- each dedicated to a different event kind(s): 0.brainstorm.ninja, 3.brainstorm.ninja, 10000.brainstorm.ninja, wot.brainstorm.ninja, wiki.brainstorm.ninja, reactions.brainstorm.ninja, 7.brainstorm.ninja, etc
- spread brand name recognition
- spam-free: only verified pubkeys can upload; will periodically 
- anyone can download (for now; may add subscription later if traffic gets too big)
- negentropy enabled; primarly long-term use will be to jump-start future Grapevine personalized relays; may restrict negentropy jump-start to Grapevine customers or verified
- architect: me

2. Centralized service that produces personalized PageRank scores and delivers by API on demand. Uses neo4j.
- runs neo4j
- periodically syncs via negentropy with Brainstorm relays
- calculates personalized pageRank on demand and offers scores by WoT DVM API
- alternative to Vertex
- main purpose: to establish relationship with main nostr clients: Primal, Amethyst, Coracle, Damus, Nostrudel, etc
- architect: need neo4j expert for ETL pipeline

3. v0.1. Personalized Nostr WoT Relay
- Alternative to centralized service; produces additional scores including Mutuals, hops, verified followers
- Further engage with major clients to interface with product to display personalized WoT scores


