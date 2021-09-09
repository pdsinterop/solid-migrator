# Solid Migrator: Possible Solutions: Forwarding

When a document is moved from one datapod to another, or more general, from one URL to another, you leave behind a file in the original location that contains a redirect instruction to the new location.

The redirect can be temporary, or permanent. As long as the original URL contains this file, applications using this URL can find the new location. This new location can potentially also contain a forwarding file with redirect instructions.

For this to work we need an ontology that allows us to express these three statements:

1. the document that used to be located at URL X is temporarily moved to URL Y. Please follow the link.

2. the document that used to be located at URL X is permanently moved to URL Y. Please update your link.

3. the document that used to be located at URL X is permanently removed. Please forget this link.

You should also be able to set a placeholder for URL X that references the URL for the containing document.

## Forwarding entities

The same ontology could also be used to forward a specific entity instead of the entire file. As long as applications that use the data understand the three possible forwarding instructions, these can be added to existing entities.

## Pro's

- No need for datapod server implementations to change
- Low impact specification. We only need to create or reuse an ontology with these three relations specified

## Con's

- Solid Apps must be written to understand the forwarding information to use this
- The original solid datapod must be available and under the owners control