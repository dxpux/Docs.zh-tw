---
title: "使用 Visual Studio for Mac 將模型新增至 Razor 頁面應用程式"
author: rick-anderson
description: "使用 Visual Studio for Mac 將模型新增至 ASP.NET Core 中的 Razor 頁面應用程式"
keywords: "ASP.NET Core, Razor 頁面, Razor,MVC, 模型"
ms.author: riande
manager: wpickett
ms.date: 08/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages-vsc/model
ms.openlocfilehash: f2f09909f4c307ce3e1a0c8571b82a709e1f88f9
ms.sourcegitcommit: 6e83c55eb0450a3073ef2b95fa5f5bcb20dbbf89
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/28/2017
---
# <a name="adding-a-model-to-a-razor-pages-app-in-aspnet-core-with-visual-studio-for-mac"></a><span data-ttu-id="b18a0-104">使用 Visual Studio for Mac 將模型新增至 ASP.NET Core 中的 Razor 頁面應用程式</span><span class="sxs-lookup"><span data-stu-id="b18a0-104">Adding a model to a Razor Pages app in ASP.NET Core with Visual Studio for Mac</span></span>

[!INCLUDE[model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="b18a0-105">新增資料模型</span><span class="sxs-lookup"><span data-stu-id="b18a0-105">Add a data model</span></span>

* <span data-ttu-id="b18a0-106">新增名為 *Models* 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="b18a0-106">Add a folder named *Models*.</span></span>
* <span data-ttu-id="b18a0-107">將類別新增至名為 *Movie.cs* 的 *Models* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b18a0-107">Add a class to the *Models* folder named *Movie.cs*.</span></span>
* <span data-ttu-id="b18a0-108">將下列程式碼新增至 *Models/Movie.cs* 檔案：</span><span class="sxs-lookup"><span data-stu-id="b18a0-108">Add the following code to the *Models/Movie.cs* file:</span></span>

[!INCLUDE[model 2](../../includes/RP/model2.md)]
[!INCLUDE[model 2a](../../includes/RP/model2a.md)]

[!code-csharp[Main](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=3-6)]

<span data-ttu-id="b18a0-109">請建置專案，以確認您沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="b18a0-109">Build the project to verify you don't have any errors.</span></span>

### <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="b18a0-110">用於移轉的 Entity Framework Core NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="b18a0-110">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="b18a0-111">[Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet) 中提供了命令列介面 (CLI) 的 EF 工具。</span><span class="sxs-lookup"><span data-stu-id="b18a0-111">The EF tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="b18a0-112">若要安裝這個套件，請將它新增至 *.csproj* 檔案中的 `DotNetCliToolReference` 集合。</span><span class="sxs-lookup"><span data-stu-id="b18a0-112">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file.</span></span> <span data-ttu-id="b18a0-113">**注意：**您必須藉由編輯 *.csproj* 檔案來安裝這個套件；而不能使用 `install-package` 命令或套件管理員 GUI。</span><span class="sxs-lookup"><span data-stu-id="b18a0-113">**Note:** You have to install this package by editing the *.csproj* file; you can't use the `install-package` command or the package manager GUI.</span></span>

<span data-ttu-id="b18a0-114">編輯 *RazorPagesMovie.csproj* 檔案：</span><span class="sxs-lookup"><span data-stu-id="b18a0-114">Edit the *RazorPagesMovie.csproj* file:</span></span>

* <span data-ttu-id="b18a0-115">選取 [檔案] > [開啟檔案]，然後選取 *RazorPagesMovie.csproj* 檔案。</span><span class="sxs-lookup"><span data-stu-id="b18a0-115">Select **File** > **Open File**, and then select the *RazorPagesMovie.csproj* file.</span></span>
* <span data-ttu-id="b18a0-116">將 `Microsoft.EntityFrameworkCore.Tools.DotNet` 的工具參考新增到第二個 **\<ItemGroup >**：</span><span class="sxs-lookup"><span data-stu-id="b18a0-116">Add tool reference for `Microsoft.EntityFrameworkCore.Tools.DotNet` to the second **\<ItemGroup>**:</span></span>

[!code-xml[Main](../../tutorials/razor-pages/razor-pages-start/snapshot_cli_sample/RazorPagesMovie/RazorPagesMovie.cli.csproj?range=12-16&highlight=4)]

[!INCLUDE[model 3](../../includes/RP/model3.md)]

<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="b18a0-117">Scaffold 電影模型</span><span class="sxs-lookup"><span data-stu-id="b18a0-117">Scaffold the Movie model</span></span>

* <span data-ttu-id="b18a0-118">在專案目錄 (包含 *Program.cs*、*Startup.cs* 和 *.csproj* 檔案的目錄) 中開啟一個命令視窗。</span><span class="sxs-lookup"><span data-stu-id="b18a0-118">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="b18a0-119">執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b18a0-119">Run the following command:</span></span>

<span data-ttu-id="b18a0-120">**注意：請在 Windows 上執行下列命令。若為 MacOS 和 Linux，請參閱下一個命令**</span><span class="sxs-lookup"><span data-stu-id="b18a0-120">**Note: Run the following command on Windows. For MacOS and Linux, see the next command**</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

* <span data-ttu-id="b18a0-121">在 MacOS 和 Linux 上，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b18a0-121">On MacOS and Linux, run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

<span data-ttu-id="b18a0-122">如果您收到錯誤：</span><span class="sxs-lookup"><span data-stu-id="b18a0-122">If you get the error:</span></span>
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

<span data-ttu-id="b18a0-123">結束 Visual Studio 並再次執行命令。</span><span class="sxs-lookup"><span data-stu-id="b18a0-123">Exit Visual Studio and run the command again.</span></span>

[!INCLUDE[model 4](../../includes/RP/model4.md)]<span data-ttu-id="b18a0-124"> 下一個教學課程說明 Scaffolding 所建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="b18a0-124"> The next tutorial explains the files created by scaffolding.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="b18a0-125">[上一步：開始使用](xref:tutorials/razor-pages-vsc/razor-pages-start)
[下一步：Scaffold Razor 頁面](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="b18a0-125">[Previous: Getting Started](xref:tutorials/razor-pages-vsc/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>