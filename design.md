# Design

The design of the library is very minimalistic, I chose to auto-generate most of the methods
since there was not a lot of variety of actions performed, except a few resources had nested ones.

Retrieved data is only parsed to JSON and response objects are generated holding information about
the status of request and next pages. Using this data model I am future proofing my library from API
changes since data retrieved from remote server is not actually validated and just held at raw form.

The main attraction here is the `.get_next` method of `Response` object that actually works with filters
provided in the original query to receive the next dataset from the current position.

Method auto-generation was chosen to avoid repeating the same code and future-proof it from adding more
resources and nested ones to the remote API.
