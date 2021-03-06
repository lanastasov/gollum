Console
=======

This producers writes messages directly to stdout or stderr.

Parameters
----------

**Enable**
  Can either be true or false to enable or disable this producer.
**Stream**
  Defines either one or an aray of stream names this producer recieves messages from.
**Channel**
  Defines the number of messages that can be buffered by the internal channel.
  By default this is set to 8192.
**ChannelTimeoutMs**
  Defines a timeout in milliseconds for messages to wait if this producer's queue is full.

  - A timeout of -1 or lower will discard the message without notice.
  - A timeout of 0 will block until the queue is free. This is the default.
  - A timeout of 1 or higher will wait n milliseconds for the queues to become available again.
    If this does not happen, the message will be send to the _DROPPED_ stream that can be processed by the :doc:`Loopback </consumers/loopback>` consumer.

**Format**
  Defines a message formatter to use. :doc:`Format.Forward </formatters/forward>` by default.
**Console**
  Either "stdout" or "stderr".

Example
-------

.. code-block:: yaml

  - "producer.Console":
    Enable: true
    Channel: 8192
    ChannelTimeoutMs: 100
    Console: "stderr"
    Stream:
        - "log"
        - "console"
