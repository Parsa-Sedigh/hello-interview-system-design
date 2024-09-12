## Section 1

Event streaming platform

can be used either as:
- message queue
- stream processing system

In order to scale, the messages require a user-specified partition strategy.

---

The problem when scaling consumers horizontally is that more than one consumer reading the same event, maybe they do it around the
same time or not. So the consumers process the event multiple times and we would get wrong results like Argentina scored multiple goals
in 80th minute!

The solution is to use consumer groups. With consumer groups, each event is guaranteed to only be processed by one consumer in the
group. Actually each partition is processed by one consumer in the consumer group.

---

Producers and consumers specify which topic they wanna work with.

Each topic can have multiple servers(brokers) holding the data of that topic.

## Section 2 - kafka overview

In kafka, the queue is called partition.

Topic is logical grouping, the grouping that exists in code. But a partition is a physical thing, a separate log file that exists on disk.

The key of a msg is also called the partition key which determines which partition the msg should go.

## Section 3 - when to use
### Streams
Note: In case of queue, the consumer gets to choose when it wants to read from the queue and therefore messages can exist in the queue
for a long time. But in case of the stream, you have an infinite stream of data that's being produced onto kafka and you need
to be consuming it as quickly as possible, so messages should be processed ASAP and would be on the queue for a short amount of time,
in order to give users real-time statistics or updates.

When we wanna a stream of msgs to be processed by multiple consumers simultaneously, this is known as pub-sub.

In kafka, the durability is discussed both when we're producing and when we're consuming:
- when producing: it's configured using ack setting(the acks are received from the leader & follower partitions)
- when consuming: it's configured with **when** the consumer commits the offset which affects the delivery semantics. At most once,
exactly once, at least once.