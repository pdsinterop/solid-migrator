# Solid Migrator

Application and specification to forward and/or move data between Solid Pods

## The Problem

While we were working on solid-nextcloud, a community solid server shut down. This server was well-used and contained a lot of datapods. While there was time to copy the data and store it somewhere else, it did a lot of damage still. All links to these satapods broke and had to be fixed manually. Not every link could be altered, for example when the owner of the datastore containing the link couldn't be reached.

*This lead to the realization that storing linked data across personal datapods all over the internet leads to a brittle system, if not mitigated.* 

Linkrot is already a large problem for the current web. In 2003 an article in the washington post quoted Brewster Kahle, of internet archive fame, who estimated that [the average lifespan of a web page was just 100 days](https://www.washingtonpost.com/archive/politics/2003/11/24/on-the-web-research-work-proves-ephemeral/959c882f-9ad0-4b36-88cd-fb7411db118d/). The first link I found was in an article that had made a cached copy of this article, to prevent linkrot I assume. In an ironic case of Murphy's Law, this cache was taken offline.

[_Read more about the problem_](problem.md)

## Possible Solutions

Based on the research mentioned below (see the "Research" section) we've formulated
what is [out of scope (things we won't do)](out-of-scope.md) and several possible solutions:

1. [Forwarding in the Data](1-forwarding.md)
2. [HTTP Status Codes](2-http.md)
3. [Meta data pod](3-meta-pod.md)
4. [Decentralized Archive/Cache](4-decentralized-cache.md)

These solutions lead to the insight that two things _must_ be created in order to
solve the problem: a **specification** and an **application**.

### Specification

Of the proposed solutions defined above, some require additions to one or more Solid specification. But the most basic specification is to create a new ontology that defines the semantics of forwarding. 

[_Read more about the proposed specification changes_](specification-changes.md)

### Solid Migrator Application

We're building the Solid Migrator as a set of [solid application tutorials](https://github.com/pdsinterop/simply-solid-app-tutorials) first. We found that all code examples for Solid are either outdated or use a complex toolchain setup. 
You can testdrive the latest version at [https://pdsinterop.org/simply-solid-app-tutorials/](https://pdsinterop.org/simply-solid-app-tutorials/10.%20UI%20Design/)

## Research  

Part of the research into the problem and possible solutions revolved around linkrot
and how it can be mitigated. Further details are available on separate pages:

### Existing attempts to mitigate linkrot

- [HTTP 300 Status and Location Header](http.md)
- [The Internet Archive and Wayback Machine](internet-archive.md)
- [DOI.org and PURL.org](url-redirect.md)
- [Perma.cc](perma.md)
- [IPFS and IPNS (and NDN)](ipfs.md)
- [Memento](memento.md)

## Team

These PDS Interop team members will be implementing the Solid Migrator [roadmap](roadmap.md):

- Auke van Slooten [@poef](//github.com/poef) - Research &amp; Specification
- Ben Peachey [@Potherca](//github.com/potherca) - Prototype Migrator
- Yvo Brevoort [@ylebre](//github.com/ylebre) - Community Outreach &amp; Server Extensions
