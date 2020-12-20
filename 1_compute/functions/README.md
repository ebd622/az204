(under construction)
# Implement Azure functions

*Quickstart: Create a Java function in Azure from the command line
https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-cli-java?tabs=bash%2Cazure-cli%2Cbrowser

*Quickstart: Create an Azure Functions project using IntelliJ IDEA
https://docs.microsoft.com/en-us/azure/developer/java/toolkit-for-intellij/quickstart-functions



#### Prerequisites: Install Azure Functions Core Tools
Azure Functions Core Tools lets you develop and test your functions on your local computer from the command prompt or terminal.
More details: https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=windows%2Ccsharp%2Cbash

### Create Azure Function from Intellij

#### 1. 
```
mvn clean package
```

#### 2. 
```
mvn azure-functions:run
```
Check in the output:

```
Azure Functions Core Tools
Core Tools Version:       3.0.3160 Commit hash: 00aa7f43cc5c5f15241b5e6e5363256f19ceb990
Function Runtime Version: 3.0.14916.0

[2020-12-20T19:39:36.014Z] Worker process started and initialized.

Functions:

        HttpExample: [GET,POST] http://localhost:7071/api/HttpExample

For detailed output, run func with --verbose flag.
```

#### 3. Open in a browser:
http://localhost:7071/api/HttpExample

http://localhost:7071/api/HttpExample?name=MyName



