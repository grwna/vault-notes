# When to Use?
- Async work: result not required immediately <-- a very important point
- Bursty traffic
- Decoupling services
- Reliability: queue holds messages, preventing loss
# Delivery Guarantee
Consumer processes a message that charges money, but crashes before it can send an ACK into the message broker. Message broker thinks it was never processed, and send it to another consumer. Now the user is charged twice. 

Delivery Guarantee is used to fix this. There are 3:
- At-Least-Once: message maybe delivered more than once (idempotency required)
- At-Most-Once: message may never arrive
- Exactly-Once: every message processed exactly once (impractical in distributed networks)
At-Least-Once is the most used for most problems.

This model also allows us to give the 'green flag' to the user, to tell them that the operation is 'done', when in reality it hasn't. Eventually that operation is **guaranteed** to be done.

# Failure Scenarios
## Poisoned Message
A message that for whatever reasons can never be succesfully processed (e.g. tryng to crop a corrupted image). This can cause infinite retries, and has to be handled. Possible solutions:
- Max retries
	- DLQ (dead letter queue), where the failed messages go, can be inspected later to see what the poison is

## Broker Crash
Solutions:
- Replica