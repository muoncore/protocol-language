# Minimal Protocol List

* [Query](http://www.fipa.org/specs/fipa00027/SC00027H.html)
* [Request when](http://www.fipa.org/specs/fipa00028/SC00028H.html)
* [Subscribe](http://www.fipa.org/specs/fipa00035/SC00035H.html)
* [Propose](http://www.fipa.org/specs/fipa00036/SC00036H.html)
* [Contract net](http://www.fipa.org/specs/fipa00029/SC00029H.html)

Next sections present a diagram and a short description extracted from FIPA website for each Interaction Protocol. Take into account that exceptions have not been included in this document. They can be found, for each protocol, in the links above.

### Query
![Query AUML Diagram](http://www.fipa.org/specs/fipa00027/SC00027H_files/image001.gif "Query AUML diagram")
Description extracted from FIPA website:
The Initiator requests the Participant to perform some kind of `inform` action using one of two query communicative acts, `query-if` or `query-ref`. The `query-if` communication is used when the Initiator wants to query whether a particular proposition is true or false and the `query-ref` communication is used when the Initiator wants to query for some identified objects. The Participant processes the `query-if` or `query-ref` and makes a decision whether to accept or refuse the query request. If the Participant makes a refuse decision, then “refused” becomes true and the Participant communicates a `refuse`. Otherwise, “agreed” becomes true.
 
If conditions indicate that an explicit agreement is required (that is, “notification necessary” is true), then the Participant communicates an `agree`. The agree may be optional depending on circumstances, for example, if the requested action is very quick and can happen before a time specified in the `reply-by` parameter. If the Participant fails, then it communicates a `failure`.
 
In a successful response, the Participant replies with one of two versions of inform:
 
* The Participant uses an `inform-t/f` communication in response to a `query-if` where the content of the `inform-t/f` asserts the truth or falsehood of the proposition, or,
 
* The Participant returns an `inform-result` communication in response to a `query-ref` and the content of the `inform-result` contains a referring expression to the objects for which the query was specified.
 
Any interaction using this interaction protocol is identified by a globally unique, non-null `conversation-id` parameter, assigned by the Initiator. The agents involved in the interaction must tag all of its ACL messages with this conversation identifier. This enables each agent to manage its communication strategies and activities, for example, it allows an agent to identify individual conversations and to reason across historical records of conversations.

### Request when
There is also the [`request`](http://www.fipa.org/specs/fipa00026/SC00026H.html) interaction protocol, which similar to this one except for the pre-condition. In request the action, if agreed, should be performed inmediately and it is not necessary to check anything. I would say Request protocol can be reproduced by Request when along a pre-condition that holds always true.

![Request when AUML Diagram](http://www.fipa.org/specs/fipa00028/SC00028H_files/image001.gif "Request when AUML diagram")

Description extracted from FIPA website:
The initiator uses the `request-when` action to request that the participant do some action once a given precondition becomes true. If the requested agent understands the request and does not initially refuse, it will agree and wait until the precondition occurs. Then, it will attempt to perform the action and notify the requester accordingly.
 
If after the initial agreement the participant is no longer able to perform the action, then it will send a failure action to the initiator. Once the action has completed and the failure, `inform-done`, or `inform-result` has been sent, the conversation ends.
 
Any interaction using this interaction protocol is identified by a globally unique, non-null `conversation-id` parameter, assigned by the Initiator. The agents involved in the interaction must tag all of its ACL messages with this conversation identifier. This enables each agent to manage its communication strategies and activities, for example, it allows an agent to identify individual conversations and to reason across historical records of conversations.

### Subscribe
![Subscribe AUML Diagram](http://www.fipa.org/specs/fipa00035/SC00035H_files/image001.gif "Subscribe AUML diagram")

Description extracted from FIPA website:
The Initiator begins the interaction with a subscribe message containing the reference of the objects in which they are interested. The Participant processes the `subscribe` message and makes a decision whether to accept or refuse the query request. If the Participant makes a refuse decision, then “refused” becomes true and the Participant communicates a `refuse`. Otherwise, ”agreed” becomes true.
 
If conditions indicate that an explicit agreement is required (that is, “notification necessary” is true), then the Participant communicates an `agree`. The agree may be optional depending on circumstances, for example, if the requested action is very quick and can happen before a time specified in the `reply-by` parameter.
 
In a successful response, the Participant replies with an `inform-result` communication with the content being a referring expression to the subscribed objects. The Participant continues to send `inform-result` messages as the objects denoted by the referring expression change. If at some point after the Participant agrees, it experiences a failure, then it communicates this with a `failure` message, which also terminates the interaction. Otherwise, the interaction may be terminated by the Initiator using the cancel meta-protocol as described in Section 1.2.
 
Any interaction using this interaction protocol is identified by a globally unique, non-null `conversation-id` parameter, assigned by the Initiator. The agents involved in the interaction must tag all of its ACL messages with this conversation identifier. This enables each agent to manage its communication strategies and activities, for example, it allows an agent to identify individual conversations and to reason across historical records of conversations. Additionally, because it may be important to preserve the sequence of the `inform-result` messages, it is important that the message transport used for this IP preserve the ordering of messages.
 
### Propose
![Propose AUML Diagram](http://www.fipa.org/specs/fipa00036/SC00036H_files/image001.gif "Propose AUML diagram")

Description extracted from FIPA website:
The Initiator sends a `propose` message to the Participant indicating that it will perform some action if the Participant agrees. The Participant responds by either accepting or rejecting the proposal, communicating this with the `accept-proposal` or `reject-proposal` communicative act, accordingly. Completion of this IP with an `accept-proposal` act would typically be followed by the performance by the Initiator of the proposed action and then the return of a status response.
 
Any interaction using this interaction protocol is identified by a globally unique, non-null `conversation-id` parameter, assigned by the Initiator. The agents involved in the interaction must tag all of its ACL messages with this conversation identifier. This enables each agent to manage its communication strategies and activities, for example, it allows an agent to identify individual conversations and to reason across historical records of conversations.
 
### Contract Net
There is a more complex version called [`Iterated Contract Net`](http://www.fipa.org/specs/fipa00030/SC00030H.html).
This protocol handles a deadline to avoid the situation where the initiator is waiting for responses indefinitely.
![Contract Net AUML Diagram](http://www.fipa.org/specs/fipa00029/SC00029H_files/image001.gif "Contract Net AUML diagram")

Description extracted from FIPA website:
The Initiator solicits m proposals from other agents by issuing a `call for proposals` (cfp) act, which specifies the task, as well any conditions the Initiator is placing upon the execution of the task. Participants receiving the `call for proposals` are viewed as potential contractors and are able to generate n responses. Of these, j are proposals to perform the task, specified as propose acts.
 
The Participant’s proposal includes the preconditions that the Participant is setting out for the task, which may be the price, time when the task will be done, etc. Alternatively, the i=n-j Participants may refuse to propose. Once the deadline passes, the Initiator evaluates the received j proposals and selects agents to perform the task; one, several or no agents may be chosen. The l agents of the selected proposal(s) will be sent an `accept-proposal` act and the remaining k agents will receive a `reject-proposal` act . The proposals are binding on the Participant, so that once the Initiator accepts the proposal, the Participant acquires a commitment to perform the task. Once the Participant has completed the task, it sends a completion message to the Initiator in the form of an `inform-done` or a more explanatory version in the form of an `inform-result`. However, if the Participant fails to complete the task, a `failure` message is sent.
 
Note that this IP requires the Initiator to know when it has received all replies. In the case that a Participant fails to reply with either a `propose` or a `refuse` act, the Initiator may potentially be left waiting indefinitely. To guard against this, the cfp act includes a deadline by which replies should be received by the Initiator. Proposals received after the deadline are automatically rejected with the given reason that the proposal was late. The deadline is specified by the reply-by parameter in the ACL message.
 
Any interaction using this interaction protocol is identified by a globally unique, non-null `conversation-id` parameter, assigned by the Initiator. The agents involved in the interaction must tag all of its ACL messages with this conversation identifier. This enables each agent to manage its communication strategies and activities, for example, it allows an agent to identify individual conversations and to reason across historical records of conversations.
 
In the case of 1:N interaction protocols or sub-protocols the Initiator is free to decide if the same `conversation-id` parameter should be used or a new one should be issued. Additionally, the messages may specify other interaction-related information such as a timeout in the `reply-by` parameter that denotes the latest time by which the sending agent would like to have received the next message in the protocol flow.
 

## Existing (Simple)

* RPC
* Introspection (rpc like)
* Event Ingest (rpc like)
* Reactive Stream

## Technical Proposed

* Pipeline
