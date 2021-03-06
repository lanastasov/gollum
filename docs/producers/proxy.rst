Proxy
=====

The proxy producer sends messages directly as-is to a given socket.
Responses from this socket are read and separated by using a specific paritioner method.
Response messages are sent back to a compatible message source like the :doc:`Proxy Consumer </consumers/proxy>`.
This can be used to create a proxy style two-way communication over Gollum.

Parameters
----------

**Enable**
    Can either be true or false to enable or disable this consumer.
**Stream**
    Defines either one or an aray of stream names this consumer sends messages to.
**Address**
  Defines the protocol, address/DNS and port to listen to.
  The protocol can either be "socket://" for unix domain or "tcp://" for TCP. UDP sockets cannot be used.
**ConnectionBufferSizeKB**
  Sets the connection buffer size in KB. By default this is set to 1024, i.e. 1 MB buffer.
  This also defines the size of the buffer used by the message parser.
**TimeoutSec**
  Defines the maximum time in seconds a client is allowed to take for a response. By default this is set to 1.
**Partitioner**
  The partitioner defines the algorithm used to separate messages from the stream.
  By default this is set to "delimiter".
   - "delimiter" separates messages by looking for a delimiter string. Thedelimiter is removed from the message.
   - "ascii" reads an ASCII encoded number at a given offset until a given delimiter is found. Everything left from and including the delimiter is removed from the message.
   - "binary" reads a binary number at a given offset and size
   - "binary_le" is an alias for "binary"
   - "binary_be" is the same as "binary" but uses big endian encoding
   - "fixed" assumes fixed size messages
**Delimiter**
  Defines the delimiter used by the "text" and "delimiter" partitioner.
  By default this is set to "\n".
**Offset**
  Defines the offset in bytes used by the binary and text paritioner.
**Size**
  Size defines the size in bytes used by the binary or fixed partitioner.
  For binary this can be set to 1,2,4 or 8. By default 4 is chosen.
  For fixed this defines the size of a message. By default 1 is chosen.

Example
-------

.. code-block:: yaml

  - "producer.Proxy":
    Enable: true
    Address: "unix:///var/gollum.socket"
    ConnectionBufferSizeKB: 64
    TimeoutSec: 3
    Partitioner: "ascii"
    Delimiter: ":"
    Offset: 1
    Stream:
      - "external"
      - "socket"
