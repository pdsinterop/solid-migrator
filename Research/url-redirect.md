# Solid Migrator: Linkrot Mitigation: URL Redirection

## DOI.org

In the field of academic publishing, the problem of linkrot is [also well known and growing](http://www.acgt.me/blog/2014/9/24/is-academic-link-rot-getting-faster-should-a-published-url-last-more-than-100-days). Articles used to be published exclusively in paper magazines, which got archived in many different libraries and online systems. There is a fixed format to reference published articles. Unfortunately, for this system that is, many articles these days are published online only. There is no paper version to archive, and the online magazines are often not long-lived. In response the publishing industry designed the DOI system, and its website https://doi.org/. Any author can request a DOI name and assign a URL to it. You can then reference the article using this DOI name. The DOI organization maintains a centralized database of names and their URLS. The original author can update this URL if the contents move. There are a lot more details to the system, but this is the simplest version.

## purl.org

Another similar service, run by the internet Archive, is called [purl.org](http://purl.org). Anyone can register for a purl.org 'domain', and add permanent URLs under the purl.org domain. These URLs then redirect to a current version of the content. The registered owner of these URL's can change them later. The contents of the target URL aren't automatically archived however.

## Pro's

- Available if the original datapod provider is offline, so you can change the redirect URL.
- Clear ownership of the original (not redirected) URL, not linked to DNS

## Con's

- Owner of the not-redirected URL (doi or purl) must keep the redirect up to date
- File level redirection only, not for sub-file entities
