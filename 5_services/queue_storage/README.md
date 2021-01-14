(Under construction)
# Implement solutions that use Azure Queue Storage queues

### Resources
* [Communicate between applications with Azure Queue storage](https://docs.microsoft.com/en-us/learn/modules/communicate-between-apps-with-azure-queue-storage/)

```java

    class Program
    {
        private const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=...";
        static void Main(string[] args)
        {
            string value = String.Join(" ", args);
            SendArticleAsync(value).Wait();
        }

        static async Task SendArticleAsync(string newsMessage)
        {
                //1. Get a storage-account
                CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

                //2. Create a queue client
                CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
                
                //3. Get a reference to a queue
                CloudQueue queue = queueClient.GetQueueReference("newsqueue");
                
                //4. Connect to a queue (or creeate it)                
                bool createdQueue = await queue.CreateIfNotExistsAsync();
                if (createdQueue)
                {
                    Console.WriteLine("The queue of news articles was created.");
                }

                //5. Create a queue-object
                CloudQueueMessage articleMessage = new CloudQueueMessage(newsMessage);
                
                //6. Add the message-object to a queue
                await queue.AddMessageAsync(articleMessage);
        }
    }

```

```java
    class Program
    {
        private const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=...";
        static void Main(string[] args)            
        {
            ReceiveArticleAsync().Wait();
        }
        static async Task<string> ReceiveArticleAsync()
        {
            CloudQueue queue = GetQueue();
            bool exists = await queue.ExistsAsync();
            if (exists)
            {
                CloudQueueMessage retrievedArticle = await queue.GetMessageAsync();
                if (retrievedArticle != null)
                {
                    string newsMessage = retrievedArticle.AsString;
                    await queue.DeleteMessageAsync(retrievedArticle);
                    Console.WriteLine($"Received {newsMessage}");
                    return newsMessage;
                }
            }
            Console.WriteLine($"Received nothing");
            return "<queue empty or not created>";
        }

        static CloudQueue GetQueue()
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
            return queueClient.GetQueueReference("newsqueue");
        }
    }
```
