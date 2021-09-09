# Solid Migrator: Possible Solutions: HTTP redirects

When a document is moved from one URL to another, you instruct the original datapod to send a HTTP redirect response when the original URL is requested.

Possible HTTP status codes are:
- [301 Moved Permanently](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/301)
- [302 Found](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/302)
- [307 Temporary Redirect](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/307)
- [308 Permanent Redirect](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/308)
- [404 Not Found](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404)
- [410 Gone](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/410)

In following the rationale for the 307/308 redirects as described on MDN, it is best to use these, instead of 301/302. They make explicit that when following the redirect, the HTTP method must not be changed.

The 404 status message is already the response of a solid datapod, when a file is not found. But we add the 410 response to explicitly allow for _right to be forgotten_ information. Meaning that it instructs the requestor that not only is the file not here, you should forget about the file entirely.

When using Solid in the browser, as almost all solid apps do, the app uses the browsers [fetch() API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch). By default [this method transparently follows redirect responses](https://developer.mozilla.org/en-US/docs/Web/API/Request/redirect). This means that when a datapod provider implements these redirect responses, there is no need to change the application code. In fact, since Solid is built on top of the web, or specifically incorporates the HTTP standard, there is no need to extend the specification to include the possible redirect status codes. They are already part of the specification.

The only problem now is how to instruct the datapod service to send these redirect responses for a given URL. We could leave this out of scope as well and let each provider implement their own solution, but this would make it difficult to write an application that could instruct a datapod to redirect a document to a new URL.

But there is already a perfectly fine specification on how to save a document in a datapod. And we have the option to save a forwarding document. So if a datapod interprets the content of a forwarding document as an instruction to send the correct HTTP message, we don't really need to add more to the specification.

This would require that datapods always interpret the incoming files though. This may be a bit too much. Datapods do something similar already with the .acl files. So we could also specify an explicit extension that is parsed as a redirect instruction by the datapod. Or we could add a .wellknown/redirects file which contains redirect instructions for the whole datapod.

**Options:**
1. Parse each file to see if it has redirect instructions.
2. Add a file.redirect (or other extension) that contains the redirect instructions.
3. Keep redirect instructions in a single file in a well-known location, e.g. .wellknown/solid-redirects.

#### 1. Parse incoming files for redirect instructions

Advantage: saving a file is already implemented and allows for seamless implementation by applications, even if the datapod doesn't support HTTP redirects. 

Disadvantage: need to parse all incoming files, leaves behind lots of files.
 
#### 2. Add a file.redirect mechanism similar to .acl files

Advantage: explicit about which files need to be parsed, similar to the .acl files.

Disadvantage: application needs to be able to see that the datapod support this, leaves behind lots of files.

One way to see if a datapod supports .redirect files is to specify that the root folder must always contain a .redirect file, even if empty. An application may then request that file and if it exists assume that it can store a file.redirect file.

#### 3. Add a .wellknown/solid-redirects file

Advantage: no added files in the datapod, applications can easily check if the datapod supports this feature. 

Disadvantage: less discoverable, needs its own UI, may become unwieldy.

Problem: A .wellknown file must be publically readable. But it may contain filenames that were never publically readable. By adding the redirect information here, potentially secret information is leaked.

Conclusion: This solution is a security risk and doesn't scale.

#### Selected option: 2 - add a file.redirect mechanism

This solution avoids the problem that a datapod must parse all incoming files to see if they contain redirect instructions. Instead the datapod only needs to parse special files, with the explicit '.redirect' extension (this extension name is provisional.)

Application support for tombstones requires a change in code in applications already. If the datapod doesn't send a HTTP redirect status message, the application must parse the returned file to see if it contains a redirect instruction.

If you are already changing application code, it isn't too much extra work to add a feature detection in the application for .redirect support in the datapod. So if an application explicitly allows the user to move/rename a file, it only needs to check for the existance of the .redirect file in the root of the datapod. If it exists, the application may assume that the datapod supports .redirect files. By appending the original filename with `.redirect` it can tell the datapod what the new location of the original file is.

If the original file is still in the datapod, this instruction should be ignored. Saving the `file.redirect` when `file` exists, must result in an error. If a `file.redirect` exists and an application saves a new `file`, the `file.redirect` must be silently removed.

If a datapod supports `.redirect` files, it must apply the same ACL instructions to this file, as it would to the original file. If the original file is writable, so must file.redirect. If the original file is readable, so must file.redirect.

The root `.redirect` file must be writable, if allowed in the ACL, as a normal file. It may contain multiple redirect statements for either files or paths, including wildcards.