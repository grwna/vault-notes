# Model
**8 Fallacies**
1. Network is reliable
2. Latency is zero
3. Bandwith is infinite
4. Network is secure
5. Topology does not change
6. One administrator
7. Transport cost is zero
8. Network is homogenous

**Properties**
- Liveness - good things eventually comes
- Safety - bad things never comes

**FLP Impossibility**
Assumptions:
1. Asynchronous Network (no time limits)
2. Deterministic Consensus
3. One Faulty Process
Indistinguishability
- Can't tell between faulty process and very slow process 
Implication
- Distributed Systems needs *trade-offs*

**Consistency Model**
- Strong
	- Linearizable
	- Sequential, can pretend that the order is a certain way, even though in reality it isn't [Notes Nau, penjelasan bagus](https://if-notes.naufarrel.tech/02.-Catatan/IF3130-Sistem-Paralel-dan-Terdistribusi/UAS/Teorema-CAP-dan-Model-Konsistensi-Data)
- Weak
	- Causal
	- Eventual

# Architecture
**Distributed System Concerns**
- Communication
- Coordination
- Scalability
- Resilience
- Operations (operational, dev, deployment, maintain, test, etc.)

**Anatomy of Distributed Systems**
- Physical
- Runtime (processes)
- Implementation (code)

**Service, Instance, Interface**
- Service: Implementation of business logic
- Instance: A running service, process from the implementation
- Interface: How services communicate with outside world
	- Inbound: requested
	- Outbound: requesting

**API and Adaper**
- API: service interface
- Adapter: translates request from/to service interface

**Architecture Styles**
- Layered (e.g. OSI layers)
- Object-based (e.g. OOP based, interactions happens though methods)

**Decoupling**
- Decouple in Space: components don't have to know each other
- Decouple in Time: components don't have to be active simultaneously
- Publish/Subscribe: publisher and subscriber (decouple in space)
- Shared Data Space: components push data to a persistent shared space, other components pull anytime (decouple in space and time)

**Centralized Architecture**: Client-Server
**Application Layering**
- UI
- Processing
- Data Layer

**Architecture Tiering**
- Single-tiered - all layers in one machine
- Two-tiered - layers separated in different machines
- Three-tiered - each layers in different machines
![[Pasted image 20251216141009.png|400]]

## Service-based Architecture
- Each service is separated
- All share the same database (different to microservices)

**NOTE**: microservices are a specific type of service-based architecture

**Function of API Gateway**
- Rate Limiting
- Routing

## Event-driven Architecture
**Request-based vs Event-driven**
- Request: synchronous (e.g REST)
- Event: asynchronous (uses a subscription model, like pub/sub decoupling)

**Event-driven Trade-offs**
overall the tradeoffs relates to how its async, and not sync + flexible and agile (can be built on easily)

## P2P Architecture
P2P is a logical network overlay

**P2P Types**
- Structured - nodes know where others are, using distributed hash table (ring, grid)
- Unstructured - nodes dont know where others are
-  Hybrid - uses superpeered to have "clustered P2P"
	- Superpeers are connected to server (client-server), regular peers are connected with the superpeer (P2P)


# Naming
Binding - relationship between the name and address (ex. 8.8.8.8 is bound to google.com)

**Directory Service**: LDAP allows resolution of addresses not just by name, but also by metadata attributes.

