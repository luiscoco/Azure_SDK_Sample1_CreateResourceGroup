# Azure_SDK_Sample1_CreateResourceGroup

This is the source code for creating a new Resource Group:

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


After creating a new Resource Group we see the following picture:

![image](https://github.com/luiscoco/Azure_SDK_Sample1_CreateResourceGroup/assets/32194879/9348c327-9d46-474d-ac08-4ee82eba415f)
