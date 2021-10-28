# Solid Migrator: Proposed Specification Changes

Of the proposed solutions, some require additions to one or more Solid specification. But the most basic specification is to create a new ontology that defines the semantics of forwarding. Specifically we need to define the semantics for:

1. This link is forwarded temporarily to X.
2. This link is forwarded permanently to X.
3. This link no longer exists.
4. This link doesn't exist and you should forget it.

In addition we may need to define

5. This link has a cached/archived copy here.
6. This archive was created at datetime.
7. This link has a content hash of X.

A link in all these cases can be a full file URL, or an entry inside a file referenced by a #id.

We're working on a new Linked Data Platform: Links (ldpl) ontology here: [https://github.com/pdsinterop/solid-link-metadata/](https://github.com/pdsinterop/solid-link-metadata/). The idea is that this ontology can be used in any linked data dataset, and applications using that data will know how to use this information to follow redirects or use archived copies. But more specifically we'll add support for this ontology in the PHP Solid Server and the Nextcloud Solid Server projects, so that if you upload a [.meta file](https://github.com/solid/solid-spec/blob/master/content-representation.md#metadata) with this information in it, the server will send appropriate HTTP redirect headers.

## Why do we need another ontology?

When researching if any current ontology comes close to this. There is the [`owl:sameAs`]() verb, but that is more commonly understood to say that two terms describe the same concept. But they may not be identical. Even worse, [the current use is not consistent](https://www.w3.org/2009/12/rdf-ws/papers/ws21).

There is another verb currently in use, but not in the normal semantic web, only to add information to webpages for use by search engines: the [`&lt;link rel="canonical"&gt;`](https://en.wikipedia.org/wiki/Canonical_link_element) tag. This is defined in the ['link relations' ontology](https://www.w3.org/2007/ont/link#) - see also [https://www.w3.org/2005/05/hrel/](https://www.w3.org/2005/05/hrel/). However this ontology is specifically written to define link types used in &lt;link rel="X"&gt; form, in e.g. HTML documents. Adding a 'redirect' type here seems wrong or at least counter-intu&iuml;tive. The link relations ontology can be found here: [https://www.w3.org/ns/iana/link-relations/relation](https://www.w3.org/ns/iana/link-relations/relation).


Finally there is a [rdfs:seeAlso](https://www.w3.org/TR/rdf-schema/#ch_seealso), but its domain is the RDF Schema itself. It is mostly used to definte terms useful in performing simple reasoning over RDF graphs. It is therefor too generic for our usecase.

Our link forwaring ontology should be clear in that it doesn't actually define any characteristic of the linked resource itself, except in purely technical fashion. e.g. "You can find the information you are looking for here."

Whether or not applications use this new ontology is not a concern of the base Solid specification. But we hope that it will become part of the recommended set of ontologies to incorporate in any Solid application.

Things are different for the datapod servers though. To support the HTTP Status code (part 2), we need a mechanism to tell the datapod server about forwarding. The simplest way is to re-use the ontology described above and combine it with a meta file similar as we can currently define ACL (Access Control Lists) in Solid. So when you upload a `myfile.forward`, the server reads that file to process forwarding instructions for `myfile`. In addition you can upload a `.forward` file in any directory, and it contains forwarding instructions for any files in that directory or subdirectories. Now when someone requests `myfile`, the datapod server can server the correct HTTP headers in the case that `myfile` itself is not available. To support this across all Solid Datapod servers, we'll have to extend the Solid specification. The [Solid WAC (Web Access Control)](https://github.com/solid/web-access-control-spec) forms a good starting point on how to do this.

The Meta datapod actually arised for free out of the forwarding ontology and server side support for it. Since you can define any forwaring link in the main `.forward` file, a datapod that only allows you to upload and edit this single file is enough to create your own permanent URL service.

The decentralized archive is supported by the last three definitions in our ontology. This will hopefully allow for archive implementations using IPFS, the internet archive or any Memento archive.
