# Protocol Internal API

This documents that API that the protocol runtime will need to present in some form to be able to run the protocols in minimal-protocol-list.md

This serves as the starter specification for the protocol language runtime.

The protocol is expected to be initialised with a configuration provided by the API.

## High Level Operations

The protocol language should be able to express the following concepts. These are expected to be implemented within the portable
language runtime, and built once.




## Primitive Operations

The above high level concepts are expected to map down to the following operations. These will be provided by the surrounding Muon runtime.
 They will be implemented once per Muon runtime.

* Open Channel to Remote.
* Close Channel
* Be notified by a Message on a channel
