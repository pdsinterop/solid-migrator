# Solid Migrator: Possible Solutions: Meta datapod

A user may prevent linkrot by creating a _meta pod_. This is a simple datapod that contains no normal files, but only a single .redirect file in the root. The meta pod responds to all requests, except for the .redirect itself, by sending a redirect response.

Such a pod is sufficiently lightweight to host, that it is possible to create a long-lived afforable service to do just this. A user can then use the URL's to this meta pod as the links in other locations. When an application requests such a link, it will receive a temporary redirect. 

The user or owner of the meta pod may at any time update these links and so move the data to another datapod, without any application having to know about it.

## Pro's

- Given support for the .redirect files, this is almost a free feature

## Con's

- Adds another hop and therefor lag to network requests
- The target file must still be available somewhere, if it isn't your own file
- Works only on URL's pointing to a full page or file, not elements inside a file.