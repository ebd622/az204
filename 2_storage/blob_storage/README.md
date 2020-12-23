(under construction)
# Develop solutions that use blob storage

#### Azure CLI
The basic commands to upload and download blobs between blob storage and the local file system are synchronous. Transferring a large blob could potentially take several hours, depending on the network bandwidth available. Additionally, if a transfer fails part-way through, there's no simple way of restarting the operation from the point of failure; you must repeat the entire operation.

#### AzCopy
A key strength of AzCopy over the Azure CLI is that all operations run asynchronously, and they're recoverable. The AzCopy command tracks the progress of copy operations, and if an operation fails, it can be restarted close to the point of failure. Additionally, you can tune the performance of the AzCopy command to match the processing power and bandwidth available to your local machine.

#### .NET Storage Client library
