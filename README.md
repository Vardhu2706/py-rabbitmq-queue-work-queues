# RabbitMQ Tutorial #2 - Work Queues (Python)

This tutorial builds on the first one and introduces Work Queues.
Instead of all messages going to a single consumer, multiple workers can share the load.

---

## Overview

- **Producer (send.py / new_task.py):** Sends messages to the durable `task_queue`.
- **Queue (task_queue):** Acts as a work queue.
- **Consumer (receive.py / worker.py):** Listens to the queue, processes messages, and acknowledges them when done.

Diagram:

```
[Producer] ---> [task_queue] ---> [Worker(s)]
```

---

## Key Points

- Queue is declared durable to survive broker restarts.
- Messages are marked as persistent (delivery_mode=2).
- Consumers use manual acknowledgements so tasks aren’t lost.
- basic_qos(prefetch_count=1) ensures fair dispatch (workers don’t get overloaded).

## Running the Example

1. Start RabbitMQ server.
2. Run one or more workers (consumers):
   python receive.py
3. Send tasks (messages) with varying workloads (dots = seconds):
   python send.py "First task."
   python send.py "Second task.."
   python send.py "Third task..."

Workers will share the load, and each dot (.) simulates one second of work.

## Reference

Tutorial #1: https://github.com/Vardhu2706/py-rabbitmq-queue-helloworld
Official tutorial: https://www.rabbitmq.com/tutorials/tutorial-two-python
