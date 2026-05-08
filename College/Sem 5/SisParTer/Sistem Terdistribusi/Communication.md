# Concepts
**Layer**
- Low-level - network layer, transport layer
- Middleware - built on top of low-level
	- Services provided by middleware
	- Communication protocols (RPC, MOM)
	- (Un)marshaling data (serialize/deserialize)
	- Naming protocols
	- Security protocols
	- Scaling mechanisms
**Communication Types**
Based on persistence
- Persistent - sent to queue (Email, SMS)
- Transient - discarded if not immediately received (Phone calls, Streams)
	- Both TCP and UDP are transient
Based on synchrony
- Async
- Sync

# Message Oriented 
**Transient**
- Example: socket (bind, listen, accept, connect)
**Persistent MOM**
- Message-oriented Middleware, persistent and asynchronouse
- Messages are put to queues, middleware is responsible for storing and sending
- Allows full decoupling
- Uses Message Broker to solvve heterogeneity of networks

# Remote Procedure Call
uses direct remote function calls

**Stub**
Makes clients think the function calls are local, when they are really remote
- Client stub - local client interface (think of OOP's interface or ABC where the implementation is in the remote)
- Server stub - unmarshaling messages into parameters

**Flow of RPC**
1. Client calls client stub
2. Client stub marshals parameter
3. Client stub makes OS send message to server
4. Server OS receives -> send to server stub
5. Server stub unmarshals message
6. Server stub calls RPC function/procedure implementation
7. Procedure returns value
8. Server sub marshals return value
9. Server sends to client
10. Client stub unmarshals

**Challenges of RPC**
- Parameters and Data
	- Cannot pass-by-reference, memory is not shared --> add referenced data to message
	- Heterogeneity of Client-Server (little/big endian and other data representation problem) --> choose standard data encoding
	- Typing
- Binding (read: DCE Binding) 
- Semantic Errors
	- At least once: RPC will be repeated until client gets a reply (good for idempotent)
	- At most once: Duplicate RPC requests will be discarded (good for non-idempotent)

**Interface Definition Language**
Language to define RPC functions, uses IDL Compiler

# Stream-Oriented
Timing is important for streams (to know which data comes first)
Stream is for unbounded data (no clear start/end) example: IoT logs, Video Live streams