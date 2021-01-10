(Under construction)
# Implement solutions that use Azure Service Bus

### Resources
* [Implement message-based communication workflows with Azure Service Bus](https://docs.microsoft.com/en-us/learn/modules/implement-message-workflows-with-service-bus/)

#### Send a message to a queue
This is a dotnet-code example from an exercise for AZ-204 preparation (**privatemessagesender**)

```java
    class Program
    {
        const string ServiceBusConnectionString = "Endpoint=sb://...";
        const string QueueName = "salesmessages";
        static IQueueClient queueClient;

        static void Main(string[] args)
        {
            SendSalesMessageAsync().GetAwaiter().GetResult();
        }

        static async Task SendSalesMessageAsync()
        {
            // 1. Create a Queue Client here
            queueClient = new QueueClient(ServiceBusConnectionString, QueueName);

            // 2. Send messages
            try
            {
                // 2. Create and send a message here
                string messageBody = $"This is a message which will be sent";
                var message = new Message(Encoding.UTF8.GetBytes(messageBody));
                await queueClient.SendAsync(message);
            }
            catch (Exception exception)
            {
                // Process an exception
            }

            // 3. Close the connection to the queue here
            await queueClient.CloseAsync();
        }
    }
```


#### Receive a message from a queue
This is a dotnet-code example from an exercise for AZ-204 preparation (**privatemessagereceiver**)

```java
    class Program
    {
        const string ServiceBusConnectionString = "Endpoint=sb://...";
        const string QueueName = "salesmessages";
        static IQueueClient queueClient;

        static void Main(string[] args)
        {
            ReceiveSalesMessageAsync().GetAwaiter().GetResult();
        }

        static async Task ReceiveSalesMessageAsync()
        {

            // 1. Create a Queue Client here
            queueClient = new QueueClient(ServiceBusConnectionString, QueueName);

            // 2. Receive a message
            RegisterMessageHandler();
        
            // 3. Close the queue here
            await queueClient.CloseAsync();

        }

        static void RegisterMessageHandler()
        {
            // 2.1
            var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
            {
                MaxConcurrentCalls = 1,
                AutoComplete = false
            };
            queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
        }

        static async Task ProcessMessagesAsync(Message message, CancellationToken token)
        {
            // 2.2
            Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
            await queueClient.CompleteAsync(message.SystemProperties.LockToken);
        }
    }
```

#### Send a message to a topic
This is a dotnet-code example from an exercise for AZ-204 preparation (**performancemessagesender**)
```java
    class Program
    {
        const string ServiceBusConnectionString = "Endpoint=sb://...";
        const string TopicName = "salesperformancemessages";
        static ITopicClient topicClient;

        static void Main(string[] args)
        {
            SendPerformanceMessageAsync().GetAwaiter().GetResult();
        }

        static async Task SendPerformanceMessageAsync()
        {
            // 1. Create a Topic Client here
            topicClient = new TopicClient(ServiceBusConnectionString, TopicName);

            // 2. Send messages
            try
            {
                // Create and send a message here
                string messageBody = $"This is a message which will be sent to a topic";
                var message = new Message(Encoding.UTF8.GetBytes(messageBody));
                await topicClient.SendAsync(message);
            }
            catch (Exception exception)
            {
                //Process an exception
            }

            // 3. Close the connection to the topic here
            await topicClient.CloseAsync();
        }
    }
```

#### Receive a message from a topic
This is a dotnet-code example from an exercise for AZ-204 preparation (**performancemessagereceiver**)

```java
    class Program
    {
        const string ServiceBusConnectionString = "Endpoint=sb://...";
        const string TopicName = "salesperformancemessages";
        const string SubscriptionName = "Americas";
        static ISubscriptionClient subscriptionClient;

        static void Main(string[] args)
        {
            MainAsync().GetAwaiter().GetResult();
        }

        static async Task MainAsync()
        {
            // 1. Create a Subscription Client here
            subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, TopicName, SubscriptionName);

            // 2. Register subscription message handler and receive messages in a loop
            RegisterMessageHandler();

            Console.Read();

            // 3. Close the subscription here
            await subscriptionClient.CloseAsync();
        }

        static void RegisterMessageHandler()
        {
            var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
            {
                MaxConcurrentCalls = 1,
                AutoComplete = false
            };
            subscriptionClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
        }

        static async Task ProcessMessagesAsync(Message message, CancellationToken token)
        {
            Console.WriteLine($"Received sale performance message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
            await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
        }

        static Task ExceptionReceivedHandler(ExceptionReceivedEventArgs exceptionReceivedEventArgs)
        {
            //Process an exception
        }  
    }
```
