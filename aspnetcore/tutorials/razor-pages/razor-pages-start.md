---
title: "開始使用 ASP.NET Core 中的 Razor 頁面"
author: rick-anderson
description: "開始使用 ASP.NET Core 中的 Razor 頁面"
keywords: "ASP.NET Core, Razor 頁面, Razor, MVC"
ms.author: riande
manager: wpickett
ms.date: 08/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 8c6e281e761e69908fc742d1f19c14a00de4bd46
ms.sourcegitcommit: 67f54fabbfa4e3942f5bfe1f8a7fdfe4a7a75358
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/19/2017
---
# <a name="getting-started-with-razor-pages-in-aspnet-core"></a><span data-ttu-id="b2e06-104">開始使用 ASP.NET Core 中的 Razor 頁面</span><span class="sxs-lookup"><span data-stu-id="b2e06-104">Getting started with Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="b2e06-105">由 [Rick Anderson](https://twitter.com/RickAndMSFT) 提供</span><span class="sxs-lookup"><span data-stu-id="b2e06-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b2e06-106">本教學課程將教導您建置 ASP.NET Core Razor 頁面之 Web 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="b2e06-106">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="b2e06-107">建議您先完成 [Razor 頁面的簡介](xref:mvc/razor-pages/index)，再開始本教學課程。</span><span class="sxs-lookup"><span data-stu-id="b2e06-107">We recommend you complete [Introduction to Razor Pages](xref:mvc/razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="b2e06-108">Razor 頁面是在 ASP.NET Core 中建置 Web 應用程式 UI 的建議方式。</span><span class="sxs-lookup"><span data-stu-id="b2e06-108">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2e06-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="b2e06-109">Prerequisites</span></span>

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="b2e06-110">建立 Razor Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b2e06-110">Create a Razor web app</span></span>

* <span data-ttu-id="b2e06-111">從 Visual Studio 的 [檔案]  功能表中，選取 [新增] > [專案] 。</span><span class="sxs-lookup"><span data-stu-id="b2e06-111">From the Visual Studio **File** menu, select **New > Project**.</span></span>
* <span data-ttu-id="b2e06-112">建立新的 ASP.NET Core Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2e06-112">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="b2e06-113">將專案命名為 **RazorPagesMovie**。</span><span class="sxs-lookup"><span data-stu-id="b2e06-113">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="b2e06-114">請務必將專案命名為 *RazorPagesMovie*，因此當您複製/貼上程式碼時，名稱空間會相符。</span><span class="sxs-lookup"><span data-stu-id="b2e06-114">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
 <span data-ttu-id="b2e06-115">![新增 ASP.NET Core Web 應用程式](../../mvc/razor-pages/index/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="b2e06-115">![new ASP.NET Core Web Application](../../mvc/razor-pages/index/_static/np.png)</span></span>
* <span data-ttu-id="b2e06-116">在下拉式清單中選取 [ASP.NET Core 2.0]，然後選取 [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2e06-116">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>
 <span data-ttu-id="b2e06-117">![Web 應用程式 (Razor 頁面)](../../mvc/razor-pages/index/_static/np2.png)</span><span class="sxs-lookup"><span data-stu-id="b2e06-117">![Web Application (Razor Pages)](../../mvc/razor-pages/index/_static/np2.png)</span></span>

<span data-ttu-id="b2e06-118">Visual Studio 範本會建立入門專案：</span><span class="sxs-lookup"><span data-stu-id="b2e06-118">The Visual Studio template creates a starter project:</span></span>

![底下提供說明，包括方案總管](razor-pages-start/_static/se.png)

<span data-ttu-id="b2e06-120">按 **F5** 在偵錯模式中執行應用程式，或按 **Ctrl-F5** 執行而不附加偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="b2e06-120">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

![Home 或 Index 頁面](razor-pages-start/_static/home.png)

* <span data-ttu-id="b2e06-122">Visual Studio 會啟動 [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview)，並執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2e06-122">Visual Studio starts [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="b2e06-123">位址列會顯示 `localhost:port#`，而不是類似於 `example.com` 的內容。</span><span class="sxs-lookup"><span data-stu-id="b2e06-123">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="b2e06-124">這是因為 `localhost` 是本機電腦的標準主機名稱。</span><span class="sxs-lookup"><span data-stu-id="b2e06-124">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="b2e06-125">Localhost 只會為來自本機電腦的 Web 要求提供服務。</span><span class="sxs-lookup"><span data-stu-id="b2e06-125">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="b2e06-126">當 Visual Studio 建立 Web 專案時，會對網頁伺服器使用隨機連接埠。</span><span class="sxs-lookup"><span data-stu-id="b2e06-126">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="b2e06-127">在上述影像中，連接埠編號為 5000。</span><span class="sxs-lookup"><span data-stu-id="b2e06-127">In the preceding image, the port number is 5000.</span></span> <span data-ttu-id="b2e06-128">當您執行應用程式時，會看到不同的連接埠編號。</span><span class="sxs-lookup"><span data-stu-id="b2e06-128">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="b2e06-129">使用 **Ctrl + F5** (非偵錯模式) 啟動應用程式，可讓您變更程式碼、儲存檔案、重新整理瀏覽器，以及查看程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="b2e06-129">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="b2e06-130">許多開發人員想要使用非偵錯模式，以便快速啟動應用程式並檢視變更。</span><span class="sxs-lookup"><span data-stu-id="b2e06-130">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE[razor-pages-start](../../includes/RP/razor-pages-start.md)]

>[!div class="step-by-step"]
[<span data-ttu-id="b2e06-131">下一步：新增模型</span><span class="sxs-lookup"><span data-stu-id="b2e06-131">Next: Adding a model</span></span>](xref:tutorials/razor-pages/modelz)  