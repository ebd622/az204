(Under construction)
# Implement solutions that use Azure Service Bus

### Resources
* [Implement message-based communication workflows with Azure Service Bus](https://docs.microsoft.com/en-us/learn/modules/implement-message-workflows-with-service-bus/)

#### Send a message to a queue



#### Receive a message
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

            RegisterMessageHandler();
        
            Console.Read();

            // Close the queue here
            await queueClient.CloseAsync();

        }

        static void RegisterMessageHandler()
        {
            var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
            {
                MaxConcurrentCalls = 1,
                AutoComplete = false
            };
            queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
        }

        static async Task ProcessMessagesAsync(Message message, CancellationToken token)
        {
            Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
            await queueClient.CompleteAsync(message.SystemProperties.LockToken);
        }
    }
```
