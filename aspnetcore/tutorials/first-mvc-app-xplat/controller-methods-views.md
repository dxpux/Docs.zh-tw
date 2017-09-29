---
title: "控制器方法和檢視"
author: rick-anderson
description: "使用控制器方法、檢視和 DataAnnotations"
keywords: ASP.NET Core,
ms.author: riande
manager: wpickett
ms.date: 04/07/2017
ms.topic: get-started-article
ms.assetid: c7313211-bb71-4adf-babe-8e72603cc0ce
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app-xplat/controller-methods-views
ms.openlocfilehash: b72fb5077d3bd577cd6282e7a6231a0806ee1fd2
ms.sourcegitcommit: 74a8ad9c1ba5c155d7c4303e67632a0922c38e86
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/20/2017
---
# <a name="controller-methods-and-views"></a><span data-ttu-id="769d6-104">控制器方法和檢視</span><span class="sxs-lookup"><span data-stu-id="769d6-104">Controller methods and views</span></span>

<span data-ttu-id="769d6-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="769d6-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="769d6-106">我們開始使用電影應用程式的情況很不錯，但呈現效果卻不理想。</span><span class="sxs-lookup"><span data-stu-id="769d6-106">We have a good start to the movie app, but the presentation is not ideal.</span></span> <span data-ttu-id="769d6-107">我們不想看到時間 (下圖的 12:00:00 AM)，而且 **ReleaseDate** 應該是兩個分開的字。</span><span class="sxs-lookup"><span data-stu-id="769d6-107">We don't want to see the time (12:00:00 AM in the image below) and **ReleaseDate** should be two words.</span></span>

![索引檢視：Release Date (發行日期) 是一個字 (不含空格)，且每個電影的發行日期均顯示 12 AM 的時間](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

<span data-ttu-id="769d6-109">開啟 *Models/Movie.cs* 檔案，然後新增反白顯示的程式碼行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="769d6-109">Open the *Models/Movie.cs* file and add the highlighted lines shown below:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDate.cs?name=snippet_1&highlight=2,11-12)]

<span data-ttu-id="769d6-110">建置和執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="769d6-110">Build and run the app.</span></span>

<!-- include start
![MVC Movie application open browser showing movie data](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

 -->

[!INCLUDE[adding-model](../../includes/mvc-intro/controller-methods-views.md)]

>[!div class="step-by-step"]
<span data-ttu-id="769d6-111">[上一步 - 使用 SQLite](working-with-sql.md)
[下一步 - 新增搜尋](search.md)</span><span class="sxs-lookup"><span data-stu-id="769d6-111">[Previous - Working with SQLite](working-with-sql.md)
[Next - Add search](search.md)</span></span>  