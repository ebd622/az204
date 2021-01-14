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
                CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

                CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

                CloudQueue queue = queueClient.GetQueueReference("newsqueue");
                bool createdQueue = await queue.CreateIfNotExistsAsync();
                if (createdQueue)
                {
                    Console.WriteLine("The queue of news articles was created.");
                }

                CloudQueueMessage articleMessage = new CloudQueueMessage(newsMessage);
                await queue.AddMessageAsync(articleMessage);
        }
    }

```

```java

    class Program
    {
    }

```
