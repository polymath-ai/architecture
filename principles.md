# Polymath Principles

- When taking a query, accept a string or an embedding, but favor the embedding. They are often chained and this way it's faster (already computed) and not repeated work.
- We are fans of the [Robustness Principle](https://en.wikipedia.org/wiki/Robustness_principle) and want to be as accepting as possible, but very explicit when we talk back (e.g. handling versions and formats)
- We favor distributed Polymath nodes that expose their endpoints, adding to the network. Polymath can be useful as a silo'd solution, but what makes it special is the interop
