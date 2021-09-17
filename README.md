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

## [Roadmap](roadmap.md)

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

We're building the solid migrator as a set of [solid application tutorials](https://github.com/pdsinterop/simply-solid-app-tutorials) first. We found that all code examples for solid are either outdated or use a very complex toolchain setup. You can testdrive the latest version at https://pdsinterop.org/simply-solid-app-tutorials/07.%20List%20Contents%20from%20Multiple%20Pods/

## Proposed Specification Changes

Of the proposed solutions defined above, some require additions to one or more Solid specification. But the most basic specification is to create a new ontology that defines the semantics of forwarding. Specifically we need to define the semantics for:

1. This link is forwarded temporarily to X.
2. This link is forwarded permanently to X.
3. This link no longer exists.
4. This link doesn't exist and you should forget it.

In addition we may need to define

5. This link has a cached/archived copy here.
6. This archive was created at datetime.
7. This link has a content hash of X.

A link in all these cases can be a full file URL, or an entry inside a file referenced by a #id.

When researching if any current ontology comes close to this. There is the [`owl:sameAs`]() verb, but that is more commonly understood to say that two terms describe the same concept. But they may not be identical. Even worse, [the current use is not consistent](https://www.w3.org/2009/12/rdf-ws/papers/ws21).

There is another verb currently in use, but not in the normal semantic web, only to add information to webpages for use by search engines: the [`&lt;link rel="canonical"&gt;`](https://en.wikipedia.org/wiki/Canonical_link_element) tag. There is no RDF ontology for this term.

Finally there is a [rdfs:seeAlso](https://www.w3.org/TR/rdf-schema/#ch_seealso), but its domain is the RDF Schema itself. It is mostly used to definte terms useful in performing simple reasoning over RDF graphs. It is therefor too generic for our usecase. 

Our link forwaring ontology should be clear in that it doesn't actually define any characteristic of the linked resource itself, except in purely technical fashion. e.g. "You can find the information you are looking for here." 

Whether or not applications use this new ontology is not a concern of the base Solid specification. But we hope that it will become part of the recommended set of ontologies to incorporate in any Solid application.

Things are different for the datapod servers though. To support the HTTP Status code (part 2), we need a mechanism to tell the datapod server about forwarding. The simplest way is to re-use the ontology described above and combine it with a meta file similar as we can currently define ACL (Access Control Lists) in Solid. So when you upload a `myfile.forward`, the server reads that file to process forwarding instructions for `myfile`. In addition you can upload a `.forward` file in any directory, and it contains forwarding instructions for any files in that directory or subdirectories. Now when someone requests `myfile`, the datapod server can server the correct HTTP headers in the case that `myfile` itself is not available. To support this across all Solid Datapod servers, we'll have to extend the Solid specification. The [Solid WAC (Web Access Control)](https://github.com/solid/web-access-control-spec) forms a good starting point on how to do this.

The Meta datapod actually arised for free out of the forwarding ontology and server side support for it. Since you can define any forwaring link in the main `.forward` file, a datapod that only allows you to upload and edit this single file is enough to create your own permanent URL service.

The decentralized archive is supported by the last three definitions in our ontology. This will hopefully allow for archive implementations using IPFS, the internet archive or any Memento archive.