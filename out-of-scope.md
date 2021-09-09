# Solid Migrator: Out of scope

## Reinvent the web protocols

Smart people at IPFS and the IETF have been working on this for years already. There is no advantage to add an extra effort here. Let's wait and see how these projects advance and use their results instead.

## Add centralized caching / archival

The whole point of Solid is to re-decentralize the web. There is no point in adding a new centralized service. If you really need it, there is always the internet archive.

## Identity migration

The ID specification is just OpenID Connect with only minor changes. To support moving ID’s we would need to seriously change that specification, with lots of impact on other applications. Or we would need to create a Solid specific specification that diverges fundamentally from the OpenID Connect specification. And the only use case is that it makes it possible to have access grants to a datapod automatically be moved to your new identity.

The risk/reward balance is not in favour of this move. You should instead just ask for access for your new identity.
