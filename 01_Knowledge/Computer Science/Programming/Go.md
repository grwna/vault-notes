# Goroutines
**Channels**
Sender -> function that sends values to channels
Receiver -> function that receives values
These are scoped per channel: sender-receiver role applies to one channel only, different channels can have different sender-receiver

Closing channels
- Channels are blocking, a receiver will wait until a channel has a value to receive
- Once a sender has no more values to send, they can close it using `close(channel_var)`
- This avoids deadlock

Goroutines functions cannot return values, this is why you use channels to move the values around.

Channel function declaration with read-write limits:
```go
func readChannel(ch <-chan int) {
	// ch is read-only
}

func writeChannel(ch chan<- int) {
	// ch is write-only
}
```

# Functions 
## Functions
## Methods
Methods are defined this way:
```go
func (t Struct) name(par1, par2 ) returnType {
}
```

Note: the `Struct` can be replaced by any user defined type.