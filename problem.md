# Solid Migrator: The Problem

While we were working on solid-nextcloud, a community solid server shut down. This server was well used and contained a lot of datapods. While there was time to copy the data and store it somewhere else, it did a lot of damage still. All links to these datapods broke and had to be fixed manually. Not every link could be altered, for example when the owner of the datastore containing the link couldn't be reached.

*This lead to the realization that storing linked data across personal datapods all over the internet leads to a brittle system, if not mitigated.* 

Linkrot is already a large problem for the current web. In 2003 an article in the washington post quoted Brewster Kahle, of internet archive fame, who estimated that [the average lifespan of a web page was just 100 days](https://www.washingtonpost.com/archive/politics/2003/11/24/on-the-web-research-work-proves-ephemeral/959c882f-9ad0-4b36-88cd-fb7411db118d/). The first link I found was in an article that had made a cached copy of this article, to prevent linkrot I assume. In an ironic case of Murphy's Law, this cache was taken offline.

## Linkrot

The term linkrot merges a number of technical and non-technical failures. The most common is that a page has been removed and requesting the URL results in a "404 Not Found" message. 

This page might also have been moved or renamed, without a proper redirect being setup. This is technically simple to do, but in general most site owners don't care that much about incoming links from other sites.

A more subtle problem occurs when the URL actually exists, but the contents have changed. Sometimes this means that the original data linked is still somewhere in the contents of the page, but more often the page has changed entirely. This can occur when the linked page is generated on the server. Blogs introduced the concept of a perma-link to identify the exact article you want to link to.

The most insidious problem occurs when the domain ownership is transferred. A company has shutdown for example, and a domain squatter has taken over the domain, usually filling it with a link farm.

## An ideal solution, that doesn't exist

In a perfect world a link from one document to another would be linked from both sides. The network or target system would know that there was an incoming link. When the target document was moved, the source document would automatically update the link. When the target document was removed, the source document could link to a network cache of the original target.

Before the web, [Xanadu](https://en.wikipedia.org/wiki/Project_Xanadu) tried to make this work, among many other features lacking in the current web. Unfortunately this resulted in such a complex system that it famously was never finished. It may be the system for which the term vaporware was invented.

## Linked Data Increases the Problem

Linkrot is already a big problem on the current web. Up to 50% of links in the Newyork Times archive are dead. Even worse, in 2013 a [paper from the Harvard Law School](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2329161), by among others Lawrence Lessig, showed that 50% of the URLs found within United States Supreme Court opinions, do not link to the originally cited information.

But the linkrot problem on the web is based on linking to specific pages or documents. When you start to use Linked Data, you link to concepts or entities contained inside pages. The use of links skyrockets because each link is much more narrowly targeted. So unless we take linkrot seriously, it may become a flaw that could be Solid's undoing.
