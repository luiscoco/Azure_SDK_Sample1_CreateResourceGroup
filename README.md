# How to create an Azure Resource Group with a .NET 8 console application and Azure SDK for .NET 

**NOTE:**
For general infor about Azure SDK for .NET navigate to the following github repo: https://github.com/Azure/azure-sdk-for-net

## 1. Open VSCode and create a new C# console application with .NET 8

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

## 2. Load the dependencies

We load the libraries/dependencies running these commands

To load the library: **Azure.Identity**

https://www.nuget.org/packages/Azure.Identity

```
dotnet add package Azure.Identity --version 1.10.4
```

To load the library: **Azure.ResourceManager** 

https://www.nuget.org/packages/Azure.ResourceManager

```
dotnet add package Azure.ResourceManager --version 1.9.0
```

For loading the library: **Azure.ResourceManager.Resources**

https://www.nuget.org/packages/Azure.ResourceManager.Resources

```
dotnet add package Azure.ResourceManager.Resources --version 1.7.0
```

Finally we load the library **Azure.ResourceManager.Storage**

https://www.nuget.org/packages/Azure.ResourceManager.Storage/1.2.0-beta.2

```
dotnet add package Azure.ResourceManager.Storage --version 1.2.0-beta.2
```

After installing the libraries we run the command:

```
dotnet restore
```

## 3. We input the application C# source code

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

## 4. Build and run the application

For executing the application we run the command:

```
dotnet run
```

## 5. See the created Resource Group in Azure portal 

After creating a new Resource Group we see the following picture:

![image](https://github.com/luiscoco/Azure_SDK_Sample1_CreateResourceGroup/assets/32194879/9348c327-9d46-474d-ac08-4ee82eba415f)
