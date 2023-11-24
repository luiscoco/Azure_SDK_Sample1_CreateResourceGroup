# How to create an Azure Resource Group with with a .NET 8 console application and Azure SDK for .NET 

We first create the folder/directory where to place our console applicaton.

```
md sampleCreatingResourceGroup
```

We navigate to the folder

```
cd sampleCreatingResourceGroup
```

We open VSCode running the command

```
code .
```

We create a .NET 8 console application with the command:

```
dotnet new console --framework net8.0
```

We load the libraries/dependencies running these commands:

```
dotnet add package Azure.Identity --version 1.10.4
```

To load the library: Azure.ResourceManager 

https://www.nuget.org/packages/Azure.ResourceManager

```
dotnet add package Azure.ResourceManager --version 1.9.0
```

After installing the libraries we run the command:

```
dotnet restore
```

We open the **program.cs** file and we input the application source code:

```csharp
using System;
using System.Threading.Tasks;
using Azure.Identity;
using Azure;
using Azure.Core;
using Azure.ResourceManager;
using Azure.ResourceManager.Resources;
using Azure.ResourceManager.Storage.Models;

ArmClient armClient = new ArmClient(new DefaultAzureCredential());
SubscriptionResource subscription = await armClient.GetDefaultSubscriptionAsync();

string rgName = "myRgNameLUISCOCO";
AzureLocation location = AzureLocation.WestEurope;
ArmOperation<ResourceGroupResource> operation = await subscription.GetResourceGroups().CreateOrUpdateAsync(WaitUntil.Completed, rgName, new ResourceGroupData(location));
ResourceGroupResource resourceGroup = operation.Value;
Console.WriteLine(resourceGroup.Data.Name);
```

For executing the application we run the command:

```
dotnet run
```

After creating a new Resource Group we see the following picture:

![image](https://github.com/luiscoco/Azure_SDK_Sample1_CreateResourceGroup/assets/32194879/9348c327-9d46-474d-ac08-4ee82eba415f)
