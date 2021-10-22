# Solid Migrator: Linkrot Mitigation: HTTP Status and Location

The web already has a standard that could prevent linkrot, through the Redirect HTTP status and the Location header. However, these require that the domain owner is willing and capable to implement them. It appears that this is not the case in general.

A good overview of [HTTP Redirection is on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Redirections).

## Status Codes

- 307 - Temporary Redirect
- 308 - Permanent Redirect
- 404 - Nothing here.
- 410 - No longer here.

## Headers

- Location

## Pro's

Solid communicates over HTTP already. So if we can induce Solid Datapod providers to send these status codes and headers, all applications will automatically follow them.

## Con's

- There is no mechanism to tell Solid Datapod providers to send forwarding headers for specific files or entities.
- The original datapod server must be available.
- The requested file or entity must not be overwritten by new, unrelated content.


