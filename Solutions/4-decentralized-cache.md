# Solid Migrator: Possible Solutions: Decentralized caching

The idea is that whenever you link to an external resource, you have the option to store a cache of the current contents of that resource somewhere else. You can then add information about that alternative source to the original link. When an application accessess your link and the external resource isn't available or valid anymore, they can choose to access the cached version instead.

The choice to use a cache, and which cache provider, is yours when you create the link. It is not builtin the network or protocol. It is optional.

You should be able to add a cryptographic hash to the linked cache to make sure the contents haven't changed since the moment you've made the cache.

## Pro's

- As long as you maintain the cache, the contents will be available
- You can cache specific entities inside a file

## Con's

- Requires additional information added to current links, we may need a new ontology just for this.
- Burden of maintaining the cache is on the party linking to a resource, there will be duplication unless you use a system that automatically deduplicates content, like IPFS.

