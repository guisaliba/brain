---
title: Glossary of terms
source: https://atproto.com/guides/glossary
description: A collection of terminology used in the AT Protocol and their definitions.
---
The AT Protocol uses a lot of terms that may not be immediately familiar. This page gives a quick reference to these terms and includes some links to more information.

## Atmosphere

The "Atmosphere" is the term we use to describe the ecosystem around the [AT Protocol](https://atproto.com/guides/#at-protocol).

## AT Protocol

The AT Protocol stands for "Authenticated Transfer Protocol," and is frequently shortened to "atproto." The name is in reference to the fact that all user-data is signed by the authoring users, which makes it possible to broadcast the data through many services and prove it's real without having to speak directly to the originating server.

The name is also a play on the "@" symbol, aka the "at" symbol, since atproto is designed for social systems.

## PDS (Personal Data Server)

A PDS, or Personal Data Server, is a server that hosts a user. A PDS will always store the user's [data repo](https://atproto.com/guides/#data-repo) and signing keys. It may also assign the user a [handle](https://atproto.com/guides/#handle) and a [DID](https://atproto.com/guides/#did-decentralized-id). Many PDSes will host multiple users.

A PDS communicates with [AppViews](https://atproto.com/guides/#app-view) to run applications. A PDS doesn't typically run any applications itself, though it will have general account management interfaces such as the OAuth login screen. PDSes actively sync their [data repos](https://atproto.com/guides/#data-repo) with [Relays](https://atproto.com/guides/#relay).

## AppView

An AppView is an application in the [Atmosphere](https://atproto.com/guides/#atmosphere). It's called an "AppView" because it's just one view of the network. The canonical data lives in [data repos](https://atproto.com/guides/#data-repo) which is hosted by [PDSes](https://atproto.com/guides/#pds-personal-data-server), and that data can be viewed many different ways.

AppViews function a bit like search engines on the Web: they aggregate data from across the Atmosphere to produce their UIs. The difference is that AppViews also communicate with users' [PDSes](https://atproto.com/guides/#pds) to publish information on their [repos](https://atproto.com/guides/#data-repo), forming the full application model. This communication is established as a part of the OAuth login flow.

## Relay

A Relay is an aggregator of [data repos](https://atproto.com/guides/#data-repo) from across the [Atmosphere](https://atproto.com/guides/#atmosphere). They sync the repos from [PDSes](https://atproto.com/guides/#pds) and produce a firehose of change events. [AppViews](https://atproto.com/guides/#app-view) use a Relay to fetch user data.

Relays are an optimization and are not strictly necessary. An [AppView](https://atproto.com/guides/#app-view) could communicate directly with [PDSes](https://atproto.com/guides/#pds) (in fact, this is encouraged if needed). The Relay serves to reduce the number of connections that are needed in the network.

## Lexicon

Lexicon is a schema language. It's used in the [Atmosphere](https://atproto.com/guides/#atmosphere) to describe [data records](https://atproto.com/guides/#record) and HTTP APIs. Functionally it's very similar to [JSON-Schema](https://json-schema.org/) and [OpenAPI](https://www.openapis.org/).

Lexicon's sole purpose is to help developers build compatible software.

- [An introduction to Lexicon](https://atproto.com/guides/lexicon)
- [Lexicon spec](https://atproto.com/specs/lexicon)

## Data Repo

The "data repository" or "repo" is the public dataset which represents a user. It is comprised of [collections](https://atproto.com/guides/#collection) of JSON [records](https://atproto.com/guides/#record) and unstructured [blobs](https://atproto.com/guides/#blob). Every repo is assigned a single permanent [DID](https://atproto.com/guides/#did-decentralized-id) which identifies it. Repos may also have any number of [domain handles](https://atproto.com/guides/#handle) which act as human-readable names.

Data repositories are signed merkle trees. Their signatures can be verified against the key material published under the repo's [did](https://atproto.com/guides/#did-decentralized-id).

- [An introduction to data repos](https://atproto.com/guides/data-repos)
- [Repository spec](https://atproto.com/specs/repository)

## Collection

The "collection" is a bucket of JSON [records](https://atproto.com/guides/#record) in a [data repository](https://atproto.com/guides/#data-repo). They support ordered list operations. Every collection is identified by an [NSID](https://atproto.com/guides/#nsid-namespaced-id) which is expected to map to a [Lexicon](https://atproto.com/guides/#lexicon) schema.

## Record

A "record" is a JSON document inside a [repo](https://atproto.com/guides/#data-repo) [collection](https://atproto.com/guides/#collection). The type of a record is identified by the `$type` field, which is expected to map to a [Lexicon](https://atproto.com/guides/#lexicon) schema. The type is also expected to match the [collection](https://atproto.com/guides/#collection) which contains it.

- [Record key spec](https://atproto.com/specs/record-key)

## Blob

Blobs are unstructured data stored inside a [repo](https://atproto.com/guides/#data-repo). They are most commonly used to store media such as images and video.

## Label

Labels are metadata objects which are attached to accounts ([DIDs](https://atproto.com/guides/#did-decentralized-id)) and [records](https://atproto.com/guides/#record). They are typically referenced by their values, such as "nudity" or "graphic-media," which identify the meaning of the label. Labels are primarily used by applications for moderation, but they can be used for other purposes.

- [Labels spec](https://atproto.com/specs/label)

## Handle

Handles are domain names which are used to identify [data repos](https://atproto.com/guides/#data-repo). More than one handle may be assigned to a repo. Handles may be used in `at://` URIs in the domain segment.

- [Handle spec](https://atproto.com/specs/handle)
- [URI Scheme spec](https://atproto.com/specs/at-uri-scheme)

## DID (Decentralized ID)

DIDs, or Decentralized IDentifiers, are universally-unique identifiers which represent [data repos](https://atproto.com/guides/#data-repo). They are permanent and non-human-readable. DIDs are a [W3C specification](https://www.w3.org/TR/did-core/). The AT Protocol currently supports `did:web` and `did:plc`, two different DID methods.

DIDs resolve to documents which contain metadata about a [repo](https://atproto.com/guides/#data-repo), including the address of the repo's [PDS](https://atproto.com/guides/#pds), the repo's [handles](https://atproto.com/guides/#handle), and the public signing keys.

- [DID spec](https://atproto.com/specs/did)

## NSID (Namespaced ID)

NSIDs, or Namespaced IDentifiers, are an identifier format used in the [Atmosphere](https://atproto.com/guides/#atmosphere) to identify [Lexicon](https://atproto.com/guides/#lexicon) schemas. They follow a reverse DNS format such as `app.bsky.feed.post`. They were chosen because they give clear schema governance via the domain ownership. The reverse-DNS format was chosen to avoid confusion with domains in URIs.

- [NSID spec](https://atproto.com/specs/nsid)

TIDs, or Timestamp IDentifiers, are an identifier format used for [record](https://atproto.com/guides/#record) keys. They are derived from the current time and designed to avoid collisions, maintain a lexicographic sort, and efficiently balance the [data repository's](https://atproto.com/guides/#data-repo) internal data structures.

- [Record keys spec](https://atproto.com/specs/record-key)

## CID (Content ID)

CIDs, or Content Identifiers, are cryptographic hashes of [records](https://atproto.com/guides/#record). They are used to track specific versions of records.

## DAG-CBOR

DAG-CBOR is a serialization format used by [atproto](https://atproto.com/guides/#at-protocol). It was chosen because it provides a reliable canonical form, which is important for cryptographic verification.

- [Data model spec](https://atproto.com/specs/data-model)

## XRPC

XRPC is [atproto's](https://atproto.com/guides/#at-protocol) HTTP API. It stands for "Cross-organizational Remote Procedure Calls" and is a thin wrapper around standard HTTPS. XRPC uses [Lexicon](https://atproto.com/guides/#lexicon) schemas to define the valid parameters and responses for each API endpoint.

- [HTTP API spec](https://atproto.com/specs/xrpc)