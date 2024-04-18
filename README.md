<details>
<summary>Tutorial Module 8</summary>

1. How many data your publlsher program will send to the message broker in one run?

    In the provided `main` function, the publisher program sends 5 data messages to the message broker in one run. Each call to `p.publish_event` sends one message, and there are five such calls in the `main` function:

    ```rust
    _ = p.publish_event("user_created".to_owned(), UserCreatedEventMessage { user_id: "1" to_owned(), user_name: "2206810042-Amir".to_owned() });
    _ = p.publish_event("user_created".to_owned(), UserCreatedEventMessage { user_id: "2" to_owned(), user_name: "2206810042-Budi".to_owned() });
    _ = p.publish_event("user_created".to_owned(), UserCreatedEventMessage { user_id: "3" to_owned(), user_name: "2206810042-Cica".to_owned() });
    _ = p.publish_event("user_created".to_owned(), UserCreatedEventMessage { user_id: "4" to_owned(), user_name: "2206810042-Dira".to_owned() });
    _ = p.publish_event("user_created".to_owned(), UserCreatedEventMessage { user_id: "5" to_owned(), user_name: "2206810042-Emir".to_owned() });
    ```

    Each call sends a unique `UserCreatedEventMessage`, resulting in a total of 5 messages being sent to the message broker.

2. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?

    The fact that both the publisher and subscriber programs are using the same AMQP URL `amqp://guest:guest@localhost:5672`, implies that they are both connecting to the same AMQP (Advanced Message Queuing Protocol) message broker.

    Here's what it means:

   - **Same Protocol (`amqp://`)**: Both programs are using the AMQP protocol for communication. This ensures compatibility and allows them to interact with the message broker using the standardized messaging protocol.

   - **Same Credentials (`guest:guest`)**: Both programs are using the same username and password (`guest:guest`) to authenticate with the message broker. This indicates that they have access permissions defined for the default guest user.

   - **Same Host and Port (`localhost:5672`)**: Both programs are connecting to the AMQP message broker hosted on the same machine (`localhost`) and using the default port number for AMQP connections, which is `5672`.

    Overall, this means that both the publisher and subscriber programs are interacting with the same messaging infrastructure, sharing the same message broker for communication. Messages published by the publisher will be sent to the same message broker, and the subscriber program will receive these messages from the same broker. This ensures that the publisher and subscriber are connected to the same messaging system and can exchange messages seamlessly.

![Screenshot of running RabbitMQ](https://i.ibb.co/02p4Y1g/gambar-2024-04-18-172837407.png)


![Screenshot of running code on console and running RabbitMQ](https://i.ibb.co/zXy9fjm/gambar-2024-04-18-173639589.png)

![Screenshot of running code on console and running RabbitMQ with spikes](https://i.ibb.co/M9TLtXG/gambar-2024-04-18-173946840.png)

The spike in RabbitMQ management console activity can be directly related to the actions performed by the publisher program. 

When the publisher program runs, it establishes connections to the RabbitMQ server specified in the AMQP URL (`amqp://guest:guest@localhost:5672`). Each call to `p.publish_event` sends a message to RabbitMQ for routing and delivery.

Here's how the publisher's actions can cause a spike in RabbitMQ management console activity:

1. **Connection Establishment**: Each time the publisher program runs, it establishes a new connection to the RabbitMQ server. This creates a spike in connection activity, visible in the RabbitMQ management console.

2. **Message Publishing**: The publisher program sends multiple messages (`UserCreatedEventMessage` instances) to RabbitMQ using the established connection. Each message sent by the publisher program results in activity within RabbitMQ, including message ingestion, routing, and potentially storage depending on RabbitMQ's configuration.

3. **Channel Activity**: In AMQP, communication occurs over channels within a connection. Each call to `p.publish_event` likely involves creating a new channel or using an existing one. This channel activity is visible in the RabbitMQ management console.

4. **Resource Utilization**: Depending on the workload and RabbitMQ's configuration, the spike in message publishing activity may result in increased resource utilization on the RabbitMQ server, such as CPU and memory usage. This can also be monitored through the management console.

In summary, the actions performed by the publisher program, such as establishing connections, sending messages, and utilizing RabbitMQ resources, directly contribute to the spike in activity observed in the RabbitMQ management console.

</details>