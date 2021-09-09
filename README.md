# solid-migrator

Solid application and specification to forward and/or move solid data

## The Problem

While we were working on solid-nextcloud, a community solid server shut down. This server was well used and contained a lot of datapods. While there was time to copy the data and store it somewhere else, it did a lot of damage still. All links to these datapods broke and had to be fixed manually. Not every link could be altered, for example when the owner of the datastore containing the link couldn't be reached.

*This lead to the realization that storing linked data across personal datapods all over the internet leads to a brittle system, if not mitigated.* 

Linkrot is already a large problem for the current web. In 2003 an article in the washington post quoted Brewster Kahle, of internet archive fame, who estimated that [the average lifespan of a web page was just 100 days](https://www.washingtonpost.com/archive/politics/2003/11/24/on-the-web-research-work-proves-ephemeral/959c882f-9ad0-4b36-88cd-fb7411db118d/). The first link I found was in an article that had made a cached copy of this article, to prevent linkrot I assume. In an ironic case of Murphy's Law, this cache was taken offline.

[Read more about the problem](problem.md)

## Team

- Ben Peachey [@Potherca](//github.com/potherca) - Prototype Migrator
- Yvo Brevoort [@ylebre](//github.com/ylebre) - Community Outreach &amp; Server Extensions
- Auke van Slooten [@poef](//github.com/poef) - Research &amp; Specification

## Existing attempts to mitigate linkrot

- [HTTP 300 Status and Location Header](http.md)
- [The Internet Archive and Wayback Machine](internet-archive.md)
- [DOI.org and PURL.org](url-redirect.md)
- [Perma.cc](perma.md)
- [IPFS and IPNS (and NDN)](ipfs.md)
- [Memento](memento.md)

## Possible Solutions

1. [Forwarding in the Data](1-forwarding.md)
2. [HTTP Status Codes](2-http.md)
3. [Meta data pod](3-meta-pod.md)
4. [Decentralized Archive/Cache](4-decentralized-cache.md)

## [Out of scope, things we won't do](out-of-scope.md)

## Prototype Solid Migrator Application

## Specification changes
