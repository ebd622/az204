(Under construction)
# Implement solutions that use Azure Service Bus

### Resources
* [Implement message-based communication workflows with Azure Service Bus](https://docs.microsoft.com/en-us/learn/modules/implement-message-workflows-with-service-bus/)

#### Send a message to a queue
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

            // Send messages.
            try
            {
                // 2. Create and send a message here
                string messageBody = $"$10,000 ebd-order for bicycle parts from retailer Adventure Works.";
                var message = new Message(Encoding.UTF8.GetBytes(messageBody));
                Console.WriteLine($"Sending message: {messageBody}");
                await queueClient.SendAsync(message);

            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} :: Exception: {exception.Message}");
            }

            // Close the connection to the queue here
            await queueClient.CloseAsync();
        }
    }
```


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
