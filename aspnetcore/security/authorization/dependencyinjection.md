---
title: 在 ASP.NET Core 需求處理常式中的相依性插入
author: rick-anderson
description: 了解如何使用相依性插入的 ASP.NET Core 應用程式中插入授權需求的處理常式。
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/dependencyinjection
ms.openlocfilehash: 4de7f0e49ade459968f8c30fbad76ce96a65815f
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="dependency-injection-in-requirement-handlers-in-aspnet-core"></a>在 ASP.NET Core 需求處理常式中的相依性插入

<a name="security-authorization-di"></a>

[授權的處理常式必須註冊](xref:security/authorization/policies#handler-registration)在設定期間的服務集合中 (使用[相依性插入](xref:fundamentals/dependency-injection#fundamentals-dependency-injection))。

假設您有想要評估之授權的處理常式內部的規則的儲存機制，該儲存機制已登錄在服務集合。 授權會解決，然後將之插入您建構函式。

例如，如果您想要使用 ASP。網路的記錄基礎結構，您會想要插入`ILoggerFactory`到您的處理常式。 這類處理常式可能如下：

```csharp
public class LoggingAuthorizationHandler : AuthorizationHandler<MyRequirement>
   {
       ILogger _logger;

       public LoggingAuthorizationHandler(ILoggerFactory loggerFactory)
       {
           _logger = loggerFactory.CreateLogger(this.GetType().FullName);
       }

       protected override Task HandleRequirementAsync(AuthorizationHandlerContext context, MyRequirement requirement)
       {
           _logger.LogInformation("Inside my handler");
           // Check if the requirement is fulfilled.
           return Task.CompletedTask;
       }
   }
   ```

您會註冊處理常式和`services.AddSingleton()`:

```csharp
services.AddSingleton<IAuthorizationHandler, LoggingAuthorizationHandler>();
```

執行個體的處理常式將您的應用程式啟動時，建立並插入已註冊的 DI 將`ILoggerFactory`到建構函式。

> [!NOTE]
> 使用 Entity Framework 的處理常式應該不會註冊為 singleton。
