---
title: "建立 Visual Studio 和 MSBuild 的發行設定檔"
author: rick-anderson
description: "說明 Visual Studio 中的 Web 發佈。"
keywords: "ASP.NET Core, Web 發佈, 發佈, msbuild, Web 部署, Dotnet 發佈, Visual Studio 2017"
ms.author: riande
manager: wpickett
ms.date: 03/14/2017
ms.topic: article
ms.assetid: 0377a02d-8fda-47a5-929a-24a16e1d2c93
ms.technology: aspnet
ms.prod: asp.net-core
uid: publishing/web-publishing-vs
ms.openlocfilehash: 665c98b5ac16bb9739af4ac204fca59a55dbb812
ms.sourcegitcommit: 78d28178345a0eea91556e4cd1adad98b1446db8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2017
---
# <a name="create-publish-profiles-for-visual-studio-and-msbuild-to-deploy-aspnet-core-apps"></a><span data-ttu-id="06de6-104">建立 Visual Studio 和 MSBuild 的發行設定檔，以部署 ASP.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="06de6-104">Create publish profiles for Visual Studio and MSBuild, to deploy ASP.NET Core apps</span></span>

<span data-ttu-id="06de6-105">作者：[Sayed Ibrahim Hashimi](https://github.com/sayedihashimi) 及 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="06de6-105">By [Sayed Ibrahim Hashimi](https://github.com/sayedihashimi) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="06de6-106">本文著重在使用 Visual Studio 2017 建立發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="06de6-106">This article focuses on using Visual Studio 2017 to create publish profiles.</span></span> <span data-ttu-id="06de6-107">使用 Visual Studio 建立的發行設定檔，可從 MSBuild 和 Visual Studio 2017 執行。</span><span class="sxs-lookup"><span data-stu-id="06de6-107">The publish profiles created with Visual Studio can be run from MSBuild and Visual Studio 2017.</span></span>

<span data-ttu-id="06de6-108">下列 *.csproj* 檔案是使用命令 `dotnet new mvc` 建立：</span><span class="sxs-lookup"><span data-stu-id="06de6-108">The following *.csproj* file was created with the command `dotnet new mvc`:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="06de6-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="06de6-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.0" />
  </ItemGroup>

  <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.0" />
  </ItemGroup>

</Project>
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="06de6-110">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="06de6-110">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp1.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore" Version="1.1.1" />
    <PackageReference Include="Microsoft.AspNetCore.Mvc" Version="1.1.2" />
    <PackageReference Include="Microsoft.AspNetCore.StaticFiles" Version="1.1.1" />
  </ItemGroup>

</Project>
```

---

<span data-ttu-id="06de6-111">上述標記的 `<Project>` 項目 (在第一行) 的 `Sdk` 屬性會進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="06de6-111">The `Sdk` attribute in the `<Project>` element (in the first line) of the markup above does the following:</span></span>

* <span data-ttu-id="06de6-112">從開始的 *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.Props* 匯入 `props` 檔案。</span><span class="sxs-lookup"><span data-stu-id="06de6-112">Imports the `props` file from *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.Props* at the beginning.</span></span>
* <span data-ttu-id="06de6-113">從結尾的 *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.targets* 匯入目標檔案。</span><span class="sxs-lookup"><span data-stu-id="06de6-113">Imports the targets file from *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.targets* at the end.</span></span>

<span data-ttu-id="06de6-114">`MSBuildSDKsPath` (與 Visual Studio 2017 Enterprise) 的預設位置在 *%programfiles(x86)%\Microsoft Visual Studio\2017\Enterprise\MSBuild\Sdks* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="06de6-114">The default location for `MSBuildSDKsPath` (with Visual Studio 2017 Enterprise) is the *%programfiles(x86)%\Microsoft Visual Studio\2017\Enterprise\MSBuild\Sdks* folder.</span></span>

<span data-ttu-id="06de6-115">`Microsoft.NET.Sdk.Web` 相依於：</span><span class="sxs-lookup"><span data-stu-id="06de6-115">`Microsoft.NET.Sdk.Web` depends on:</span></span>

* <span data-ttu-id="06de6-116">*Microsoft.NET.Sdk.Web.ProjectSystem*</span><span class="sxs-lookup"><span data-stu-id="06de6-116">*Microsoft.NET.Sdk.Web.ProjectSystem*</span></span>
* <span data-ttu-id="06de6-117">*Microsoft.NET.Sdk.Publish*</span><span class="sxs-lookup"><span data-stu-id="06de6-117">*Microsoft.NET.Sdk.Publish*</span></span>

<span data-ttu-id="06de6-118">這會導致匯入下列 `props` 和 `targets`：</span><span class="sxs-lookup"><span data-stu-id="06de6-118">Which causes the following `props` and `targets` to be imported:</span></span>

* <span data-ttu-id="06de6-119">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.Props</span><span class="sxs-lookup"><span data-stu-id="06de6-119">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.Props</span></span>
* <span data-ttu-id="06de6-120">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.targets</span><span class="sxs-lookup"><span data-stu-id="06de6-120">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.targets</span></span>
* <span data-ttu-id="06de6-121">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.Props</span><span class="sxs-lookup"><span data-stu-id="06de6-121">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.Props</span></span>
* <span data-ttu-id="06de6-122">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.targets</span><span class="sxs-lookup"><span data-stu-id="06de6-122">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.targets</span></span>

<span data-ttu-id="06de6-123">發佈目標會再次根據所使用的發佈方法，匯入正確的目標集。</span><span class="sxs-lookup"><span data-stu-id="06de6-123">Publish targets will again import the right set of targets based on the publish method used.</span></span>

<span data-ttu-id="06de6-124">當 MSBuild 或 Visual Studio 載入專案時，會執行下列高階動作：</span><span class="sxs-lookup"><span data-stu-id="06de6-124">When MSBuild or Visual Studio loads a project, the following high level actions are performed:</span></span>

* <span data-ttu-id="06de6-125">建置專案</span><span class="sxs-lookup"><span data-stu-id="06de6-125">Build project</span></span>
* <span data-ttu-id="06de6-126">計算要發佈的檔案</span><span class="sxs-lookup"><span data-stu-id="06de6-126">Compute files to publish</span></span>
* <span data-ttu-id="06de6-127">將檔案發佈至目的地</span><span class="sxs-lookup"><span data-stu-id="06de6-127">Publish files to destination</span></span>

### <a name="compute-project-items"></a><span data-ttu-id="06de6-128">計算專案項目</span><span class="sxs-lookup"><span data-stu-id="06de6-128">Compute project items</span></span>

<span data-ttu-id="06de6-129">載入專案時，會計算專案項目 (檔案)。</span><span class="sxs-lookup"><span data-stu-id="06de6-129">When the project is loaded, the project items (files) are computed.</span></span> <span data-ttu-id="06de6-130">`item type` 屬性會決定如何處理檔案。</span><span class="sxs-lookup"><span data-stu-id="06de6-130">The `item type` attribute determines how the file is processed.</span></span> <span data-ttu-id="06de6-131">根據預設，*.cs* 檔案會包含在 `Compile` 項目清單中。</span><span class="sxs-lookup"><span data-stu-id="06de6-131">By default, *.cs* files are included in the `Compile` item list.</span></span> <span data-ttu-id="06de6-132">`Compile` 項目清單中的檔案會予以編譯。</span><span class="sxs-lookup"><span data-stu-id="06de6-132">Files in the `Compile` item list are compiled.</span></span>

<span data-ttu-id="06de6-133">`Content` 項目清單包含的檔案還會另行發佈到組建輸出。</span><span class="sxs-lookup"><span data-stu-id="06de6-133">The `Content` item list contains files that will be published in addition to the build outputs.</span></span> <span data-ttu-id="06de6-134">根據預設，符合模式 wwwroot/** 的檔案會包含在 `Content` 項目中。</span><span class="sxs-lookup"><span data-stu-id="06de6-134">By default, files matching the pattern wwwroot/** will be included in the `Content` item.</span></span> <span data-ttu-id="06de6-135">[wwwroot/** 是通用慣例模式](https://gruntjs.com/configuring-tasks#globbing-patterns)，指定 *wwwroot* 資料夾**和**子資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="06de6-135">[wwwroot/** is a globbing pattern](https://gruntjs.com/configuring-tasks#globbing-patterns) that specifies all files in the *wwwroot* folder **and** subfolders.</span></span> <span data-ttu-id="06de6-136">如果您需要明確地將檔案新增至發佈清單，您可以直接在 *.csproj* 檔案中新增檔案，如[包括檔案](#including-files)中所示。</span><span class="sxs-lookup"><span data-stu-id="06de6-136">If you need to explicitly add a file to the publish list you can add the file directly in the *.csproj* file as shown in [Including Files](#including-files).</span></span>

<span data-ttu-id="06de6-137">當您在 Visual Studio 中選取 [發佈] 按鈕，或當您從命令列發佈時：</span><span class="sxs-lookup"><span data-stu-id="06de6-137">When you select the **Publish** button in Visual Studio or when you publish from command line:</span></span>

- <span data-ttu-id="06de6-138">會計算屬性/項目 (需要建置的檔案)。</span><span class="sxs-lookup"><span data-stu-id="06de6-138">The properties/items are computed (the files that are needed to build).</span></span>
- <span data-ttu-id="06de6-139">僅限 Visual Studio：還原 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="06de6-139">Visual Studio only: NuGet packages are restored.</span></span>  <span data-ttu-id="06de6-140">(CLI 的使用者要明確還原。)</span><span class="sxs-lookup"><span data-stu-id="06de6-140">(Restore needs to be explicit by the user on the CLI.)</span></span>
- <span data-ttu-id="06de6-141">專案隨即建置。</span><span class="sxs-lookup"><span data-stu-id="06de6-141">The project builds.</span></span>
- <span data-ttu-id="06de6-142">會計算的發佈項目 (需要發佈的檔案)。</span><span class="sxs-lookup"><span data-stu-id="06de6-142">The publish items are computed (the files that are needed to publish).</span></span>
- <span data-ttu-id="06de6-143">專案已發佈。</span><span class="sxs-lookup"><span data-stu-id="06de6-143">The project is published.</span></span> <span data-ttu-id="06de6-144">(計算的檔案會複製到發佈目的地。)</span><span class="sxs-lookup"><span data-stu-id="06de6-144">(The computed files are copied to the publish destination.)</span></span>

## <a name="simple-command-line-publishing"></a><span data-ttu-id="06de6-145">簡單的命令列發佈</span><span class="sxs-lookup"><span data-stu-id="06de6-145">Simple command line publishing</span></span>

<span data-ttu-id="06de6-146">本節適用於所有 .NET Core 支援的平台，不需要 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="06de6-146">This section works on all .NET Core supported platforms and doesn't require Visual Studio.</span></span> <span data-ttu-id="06de6-147">在下列範例中，`dotnet publish` 命令是從專案目錄執行 (其包含 *.csproj* 檔案)。</span><span class="sxs-lookup"><span data-stu-id="06de6-147">In the samples below, the `dotnet publish` command is run from the project directory (which contains the *.csproj* file).</span></span> <span data-ttu-id="06de6-148">如果您不在專案資料夾中，您可以明確方式在專案檔案路徑中傳送。</span><span class="sxs-lookup"><span data-stu-id="06de6-148">If you're not in the project folder, you can explicitly pass in the project file path.</span></span> <span data-ttu-id="06de6-149">例如: </span><span class="sxs-lookup"><span data-stu-id="06de6-149">For example:</span></span>

```console
dotnet publish  c:/webs/web1
```

<span data-ttu-id="06de6-150">執行下列命令來建立及發佈 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="06de6-150">Run the following commands to create and publish a web app:</span></span>

```console
dotnet new mvc
dotnet restore
dotnet publish
```

<span data-ttu-id="06de6-151">`dotnet publish` 會產生與類似下列內容的輸出：</span><span class="sxs-lookup"><span data-stu-id="06de6-151">The `dotnet publish` produces output similar to the following:</span></span>

```console
C:\Webs\Web1>dotnet publish
Microsoft (R) Build Engine version 15.1.548.43366
Copyright (C) Microsoft Corporation. All rights reserved.

  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp1.1\Web1.dll
```

<span data-ttu-id="06de6-152">預設發佈資料夾是 `bin\$(Configuration)\netcoreapp<version>\publish`。</span><span class="sxs-lookup"><span data-stu-id="06de6-152">The default publish folder is `bin\$(Configuration)\netcoreapp<version>\publish`.</span></span> <span data-ttu-id="06de6-153">`$(Configuration)` 預設為偵錯。</span><span class="sxs-lookup"><span data-stu-id="06de6-153">The default for `$(Configuration)` is Debug.</span></span> <span data-ttu-id="06de6-154">在上例中，`<TargetFramework>` 是 `netcoreapp1.1`。</span><span class="sxs-lookup"><span data-stu-id="06de6-154">In the sample above, the `<TargetFramework>` is `netcoreapp1.1`.</span></span> <span data-ttu-id="06de6-155">上例中的實際路徑是 *bin\Debug\netcoreapp1.1\publish*。</span><span class="sxs-lookup"><span data-stu-id="06de6-155">The actual path in the sample above is *bin\Debug\netcoreapp1.1\publish*.</span></span>

<span data-ttu-id="06de6-156">`dotnet publish -h` 顯示發佈的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="06de6-156">`dotnet publish -h` displays help information for publish.</span></span>

<span data-ttu-id="06de6-157">下列命令會指定 `Release` 組建和發佈目錄：</span><span class="sxs-lookup"><span data-stu-id="06de6-157">The following command specifies a `Release` build and the publishing directory:</span></span>

```console
dotnet publish -c Release -o C:/MyWebs/test
```

<span data-ttu-id="06de6-158">`dotnet publish` 命令會呼叫 `MSBuild`，後者叫用 `Publish` 目標。</span><span class="sxs-lookup"><span data-stu-id="06de6-158">The `dotnet publish` command calls `MSBuild` which invokes the `Publish` target.</span></span> <span data-ttu-id="06de6-159">任何傳遞至 `dotnet publish` 的參數都會傳遞至 `MSBuild`。</span><span class="sxs-lookup"><span data-stu-id="06de6-159">Any parameters passed to `dotnet publish` are passed to `MSBuild`.</span></span> <span data-ttu-id="06de6-160">`-c` 參數對應至 `Configuration` MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="06de6-160">The `-c` parameter maps to the `Configuration` MSBuild property.</span></span> <span data-ttu-id="06de6-161">`-o` 參數對應至 `OutputPath`。</span><span class="sxs-lookup"><span data-stu-id="06de6-161">The `-o` parameter maps to `OutputPath`.</span></span>

<span data-ttu-id="06de6-162">您可以使用下列兩種格式之一傳遞 MSBuild 屬性：</span><span class="sxs-lookup"><span data-stu-id="06de6-162">You can pass MSBuild properties using either of the following formats:</span></span>

- ` p:<NAME>=<VALUE>`
- `/p:<NAME>=<VALUE>`

<span data-ttu-id="06de6-163">下列命令會將 `Release` 組建發佈到網路共用：</span><span class="sxs-lookup"><span data-stu-id="06de6-163">The following command publishes a `Release` build to a network share:</span></span>

`dotnet publish -c Release /p:PublishDir=//r8/release/AdminWeb`

<span data-ttu-id="06de6-164">網路共用以正斜線 (*//r8/*) 指定，適用於所有 .NET Core 支援的平台。</span><span class="sxs-lookup"><span data-stu-id="06de6-164">The network share is specified with forward slashes (*//r8/*) and works on all .NET Core supported platforms.</span></span>

<span data-ttu-id="06de6-165">確認部署的已發佈應用程式未在執行中。</span><span class="sxs-lookup"><span data-stu-id="06de6-165">Confirm that the published app for deployment isn't running.</span></span> <span data-ttu-id="06de6-166">當應用程式執行時，會鎖定 *publish* 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="06de6-166">Files in the *publish* folder are locked when the app is running.</span></span> <span data-ttu-id="06de6-167">因為無法複製鎖定的檔案，所以無法執行部署。</span><span class="sxs-lookup"><span data-stu-id="06de6-167">Deployment can't occur because locked files can't be copied.</span></span>

## <a name="publish-profiles"></a><span data-ttu-id="06de6-168">發行設定檔</span><span class="sxs-lookup"><span data-stu-id="06de6-168">Publish profiles</span></span>

<span data-ttu-id="06de6-169">本節會使用 Visual Studio 2017 及更高版本建立發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="06de6-169">This section uses Visual Studio 2017 and higher to create publishing profiles.</span></span> <span data-ttu-id="06de6-170">建立之後，您就可以從 Visual Studio 或命令列發佈。</span><span class="sxs-lookup"><span data-stu-id="06de6-170">Once created, you can publish from Visual Studio or the command line.</span></span>

<span data-ttu-id="06de6-171">發行設定檔可簡化發佈程序。</span><span class="sxs-lookup"><span data-stu-id="06de6-171">Publish profiles can simplify the publishing process.</span></span> <span data-ttu-id="06de6-172">您可以有多個發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="06de6-172">You can have multiple publish profiles.</span></span> <span data-ttu-id="06de6-173">若要在 Visual Studio 中建立發行設定檔，以滑鼠右鍵按一下方案總管中的專案，然後選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="06de6-173">To create a publish profile in Visual Studio, right click on the project in Solution Explore and select **Publish**.</span></span> <span data-ttu-id="06de6-174">或者，您可以從 [建置] 功能表選取 [發佈 \<專案名稱>] 。</span><span class="sxs-lookup"><span data-stu-id="06de6-174">Alternatively, you can select **Publish     \<project name>** from the build menu.</span></span> <span data-ttu-id="06de6-175">隨即顯示應用程式容量頁面的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="06de6-175">The **Publish** tab of the application capacities page is displayed.</span></span> <span data-ttu-id="06de6-176">如果專案不包含發行設定檔，則會顯示下列頁面：</span><span class="sxs-lookup"><span data-stu-id="06de6-176">If the project doesn't contain a publish profile, the following page is displayed:</span></span>

![應用程式容量頁面的 [發佈]**** 索引標籤，顯示選取了 Azure、IIS、FTB，資料夾與 Azure。](web-publishing-vs/_static/az.png)

<span data-ttu-id="06de6-179">選取 [資料夾] 時，[發佈] 按鈕會建立並發佈發行設定檔資料夾。</span><span class="sxs-lookup"><span data-stu-id="06de6-179">When **Folder** is selected, the **Publish** button creates a folder publish profile and publishes.</span></span>

![應用程式容量頁面的 [發佈]**** 索引標籤，顯示 Azure、IIS、FTB、資料夾。](web-publishing-vs/_static/pub1.png)

<span data-ttu-id="06de6-181">一旦建立發行設定檔，[發佈] 索引標籤即會變更，而您要選取 [建立新的設定檔] 來建立新的設定檔。</span><span class="sxs-lookup"><span data-stu-id="06de6-181">Once a publish profile is created, the **Publish** tab changes, and you select **Create new profile** to create a new profile.</span></span>

![應用程式容量頁面 [發佈]**** 索引標籤：顯示在最後一個步驟中建立的 FolderProfile，以及建立新的設定檔連結。](web-publishing-vs/_static/create_new.png)

<span data-ttu-id="06de6-183">發佈精靈支援下列發佈目標：</span><span class="sxs-lookup"><span data-stu-id="06de6-183">The Publish wizard supports the following publish targets:</span></span>

- <span data-ttu-id="06de6-184">Microsoft Azure App Service</span><span class="sxs-lookup"><span data-stu-id="06de6-184">Microsoft Azure App Service</span></span>
- <span data-ttu-id="06de6-185">IIS、FTP 等等 (適用於任何網頁伺服器)</span><span class="sxs-lookup"><span data-stu-id="06de6-185">IIS, FTP, etc (for any web server)</span></span>
- <span data-ttu-id="06de6-186">資料夾</span><span class="sxs-lookup"><span data-stu-id="06de6-186">Folder</span></span>
- <span data-ttu-id="06de6-187">匯入設定檔 (可讓您匯入設定檔)。</span><span class="sxs-lookup"><span data-stu-id="06de6-187">Import profile (allows you to import a profile).</span></span>
- <span data-ttu-id="06de6-188">Microsoft Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="06de6-188">Microsoft Azure Virtual Machines</span></span>

<span data-ttu-id="06de6-189">如需詳細資訊，請參閱[哪些發佈選項適合我？](https://docs.microsoft.com/visualstudio/ide/not-in-toc/web-publish-options)</span><span class="sxs-lookup"><span data-stu-id="06de6-189">See [What publishing options are right for me?](https://docs.microsoft.com/visualstudio/ide/not-in-toc/web-publish-options) for more information.</span></span>

<span data-ttu-id="06de6-190">當您使用 Visual Studio 建立發行設定檔時，會建立 *Properties/PublishProfiles/\<發佈名稱>.pubxml* 的 MSBuild 檔案。</span><span class="sxs-lookup"><span data-stu-id="06de6-190">When you create a publish profile with Visual Studio, a *Properties/PublishProfiles/\<publish name>.pubxml* MSBuild file is created.</span></span> <span data-ttu-id="06de6-191">這個 *.pubxml* 檔案是 MSBuild 檔案，而且包含發佈組態設定。</span><span class="sxs-lookup"><span data-stu-id="06de6-191">This *.pubxml* file is a MSBuild file and contains publish configuration settings.</span></span> <span data-ttu-id="06de6-192">您可以變更這個檔案以自訂建置和發佈處理序。</span><span class="sxs-lookup"><span data-stu-id="06de6-192">You can change this file to customize the build and publish process.</span></span> <span data-ttu-id="06de6-193">發佈程序會讀取這個檔案。</span><span class="sxs-lookup"><span data-stu-id="06de6-193">This file is read by the publishing process.</span></span> <span data-ttu-id="06de6-194">`<LastUsedBuildConfiguration>` 很特殊，因為它是全域屬性，不應該在組建匯入的任何檔案中。</span><span class="sxs-lookup"><span data-stu-id="06de6-194">`<LastUsedBuildConfiguration>` is special because it’s a global property and shouldn’t be in any file that’s imported in the build.</span></span> <span data-ttu-id="06de6-195">如需詳細資訊，請參閱 [MSBuild：如何設定組態屬性](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)。</span><span class="sxs-lookup"><span data-stu-id="06de6-195">See [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) for more info.</span></span>
<span data-ttu-id="06de6-196">*.pubxml* 檔案不應該簽入原始檔控制，因為它會隨 *.user* 檔案而定。</span><span class="sxs-lookup"><span data-stu-id="06de6-196">The *.pubxml* file should not be checked into source control because it depends on the *.user* file.</span></span> <span data-ttu-id="06de6-197">*.user* 檔案絕對不能簽入原始檔控制，因為它可以包含機密資訊，而且只對一位使用者和一部電腦有效。</span><span class="sxs-lookup"><span data-stu-id="06de6-197">The *.user* file should never be checked into source control because it can contain sensitive information and it's only valid for one user and machine.</span></span>

<span data-ttu-id="06de6-198">機密資訊 (例如發佈密碼) 是依每個使用者/電腦加密，且儲存在 *Properties/PublishProfiles/*\<發佈名稱>.pubxml.user 檔案中。</span><span class="sxs-lookup"><span data-stu-id="06de6-198">Sensitive information (like the publish password) is encrypted on a per user/machine level and stored in the *Properties/PublishProfiles/\<publish name>.pubxml.user* file.</span></span> <span data-ttu-id="06de6-199">因為這個檔案可以包含機密資訊，所以它「不」應該簽入原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="06de6-199">Because this file can contain sensitive information, it should **not** be checked into source control.</span></span>

<span data-ttu-id="06de6-200">如需如何在 ASP.NET Core 上發佈 Web 應用程式的概觀，請參閱[發佈和部署](index.md)。</span><span class="sxs-lookup"><span data-stu-id="06de6-200">For an overview of how to publish a web app on ASP.NET Core see [Publishing and Deployment](index.md).</span></span> <span data-ttu-id="06de6-201">[發佈和部署](index.md)是開放原始碼專案，位在 https://github.com/aspnet/websdk。</span><span class="sxs-lookup"><span data-stu-id="06de6-201">[Publishing and Deployment](index.md) is an open source project at https://github.com/aspnet/websdk.</span></span>

<span data-ttu-id="06de6-202">目前 `dotnet publish` 不能使用發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="06de6-202">Currently `dotnet publish` doesn’t have the ability to use publish profiles.</span></span> <span data-ttu-id="06de6-203">若要使用發行設定檔，請使用 `dotnet build`。</span><span class="sxs-lookup"><span data-stu-id="06de6-203">To use publish profiles, use `dotnet build`.</span></span> <span data-ttu-id="06de6-204">`dotnet build` 在專案上叫用 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="06de6-204">`dotnet build` invokes MSBuild on the project.</span></span> <span data-ttu-id="06de6-205">或者，直接呼叫 `msbuild`。</span><span class="sxs-lookup"><span data-stu-id="06de6-205">Alternatively, call `msbuild` directly.</span></span>

<span data-ttu-id="06de6-206">使用發行設定檔時，請設定下列 MSBuild 屬性：</span><span class="sxs-lookup"><span data-stu-id="06de6-206">Set the following MSBuild properties when using a publish profile:</span></span>

- `DeployOnBuild=true`
- `PublishProfile=<Publish profile name>`

<span data-ttu-id="06de6-207">例如，當發行名為 *FolderProfile* 的設定檔時，您可以執行下列命令之一。</span><span class="sxs-lookup"><span data-stu-id="06de6-207">For example, when publishing with a profile named *FolderProfile* you can execute either of the commands below.</span></span>

- `dotnet build /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`
- `msbuild      /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`

<span data-ttu-id="06de6-208">當您叫用 `dotnet build` 時，它會呼叫 `msbuild` 來執行建置和發佈程序。</span><span class="sxs-lookup"><span data-stu-id="06de6-208">When you invoke `dotnet build` it will call `msbuild` to run the build and publish process.</span></span> <span data-ttu-id="06de6-209">當您傳入資料夾設定檔時，呼叫 `dotnet build` 或 `msbuild` 基本上是一樣的。</span><span class="sxs-lookup"><span data-stu-id="06de6-209">Calling `dotnet build` or `msbuild` is essentially equivalent when you pass in a folder profile.</span></span> <span data-ttu-id="06de6-210">直接在 Windows 上呼叫 MSBuild 時，您會取得 .NET Framework 版本的 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="06de6-210">When calling MSBuild directly on Windows you get the .NET Framework version of MSBuild.</span></span>  <span data-ttu-id="06de6-211">MSDeploy 目前僅限於 Windows 電腦進行發佈。</span><span class="sxs-lookup"><span data-stu-id="06de6-211">MSDeploy is currently limited to Windows machines for publishing.</span></span> <span data-ttu-id="06de6-212">在非資料夾設定檔上呼叫 `dotnet build` 會叫用 MSBuild，而 MSBuild 會在非資料夾設定檔上使用 MSDeploy。</span><span class="sxs-lookup"><span data-stu-id="06de6-212">Calling `dotnet build` on a non-folder profile invokes MSBuild, and MSBuild uses MSDeploy on non-folder profiles.</span></span> <span data-ttu-id="06de6-213">在非資料夾設定檔上呼叫 `dotnet build`，會叫用 MSBuild (使用 MSDeploy) 並造成失敗 (即使是在 Windows 平台上執行)。</span><span class="sxs-lookup"><span data-stu-id="06de6-213">Calling `dotnet build` on a non-folder profile invokes MSBuild (using MSDeploy) and results in a failure (even when running on a Windows platform).</span></span> <span data-ttu-id="06de6-214">若要發佈非資料夾的設定檔，請直接呼叫 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="06de6-214">To publish with a non-folder profile, call MSBuild directly.</span></span>

<span data-ttu-id="06de6-215">下列資料夾發行設定檔是以 Visual Studio 建立並發佈至網路共用：</span><span class="sxs-lookup"><span data-stu-id="06de6-215">The following folder publish profile was created with Visual Studio and publishes to a network share:</span></span>

[!code-xml[Main](web-publishing-vs/sample/FolderProfile.pubxml?highlight=5,9,11,18)]

<span data-ttu-id="06de6-216">請注意，`<LastUsedBuildConfiguration>` 設定為 `Release`。</span><span class="sxs-lookup"><span data-stu-id="06de6-216">Note `<LastUsedBuildConfiguration>` is set to `Release`.</span></span>  <span data-ttu-id="06de6-217">從 Visual Studio 發佈時，會使用發佈程序開始時的值來設定 `<LastUsedBuildConfiguration>` 組態屬性值。</span><span class="sxs-lookup"><span data-stu-id="06de6-217">When publishing from Visual Studio, the `<LastUsedBuildConfiguration>` configuration property value is set using the value when the publish process is started.</span></span> <span data-ttu-id="06de6-218">`<LastUsedBuildConfiguration>` 組態屬性很特殊，不應在匯入的 MSBuild 檔案中覆寫。</span><span class="sxs-lookup"><span data-stu-id="06de6-218">The `<LastUsedBuildConfiguration>` configuration property is special and shouldn’t be overridden in an imported MSBuild file.</span></span> <span data-ttu-id="06de6-219">您可以從命令列覆寫這個屬性。</span><span class="sxs-lookup"><span data-stu-id="06de6-219">You can override this property from the command line.</span></span> <span data-ttu-id="06de6-220">例如: </span><span class="sxs-lookup"><span data-stu-id="06de6-220">For example:</span></span>

`dotnet build -c Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`

<span data-ttu-id="06de6-221">使用 MSBuild：</span><span class="sxs-lookup"><span data-stu-id="06de6-221">Using MSBuild:</span></span>

`msbuild /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`

## <a name="publish-to-an-msdeploy-endpoint-from-the-command-line"></a><span data-ttu-id="06de6-222">從命令列發佈至 MSDeploy 端點</span><span class="sxs-lookup"><span data-stu-id="06de6-222">Publish to an MSDeploy endpoint from the command line</span></span>

<span data-ttu-id="06de6-223">如先前所述，您可以使用 `dotnet publish` 或 `msbuild` 命令發佈。</span><span class="sxs-lookup"><span data-stu-id="06de6-223">As previously mentioned, you can publish using `dotnet publish` or the `msbuild` command.</span></span> <span data-ttu-id="06de6-224">`dotnet publish` 在 .NET Core 的內容中執行。</span><span class="sxs-lookup"><span data-stu-id="06de6-224">`dotnet publish` runs in the context of .NET Core.</span></span> <span data-ttu-id="06de6-225">`msbuild` 需要 .NET framework，因此限於 Windows 環境。</span><span class="sxs-lookup"><span data-stu-id="06de6-225">`msbuild` requires .NET framework, and is therefore limited to Windows environments.</span></span>

<span data-ttu-id="06de6-226">以 MSDeploy 發佈最簡單的方式，是先在 Visual Studio 2017 中建立發行設定檔，再從命令列使用設定檔。</span><span class="sxs-lookup"><span data-stu-id="06de6-226">The easiest way to publish with MSDeploy is to first create a publish profile in Visual Studio 2017 and use the profile from the command line.</span></span>

<span data-ttu-id="06de6-227">在下列範例中，我建立了 ASP.NET Core Web 應用程式 (使用 `dotnet new mvc`)，並使用 Visual Studio 新增了 Azure 發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="06de6-227">In the following sample, I created an ASP.NET Core web app ( using `dotnet new mvc`) and added an Azure publish profile with Visual Studio.</span></span>

<span data-ttu-id="06de6-228">您從 **VS 2017 開發人員命令提示字元**執行 `msbuild`。</span><span class="sxs-lookup"><span data-stu-id="06de6-228">You run `msbuild` from a **Developer Command Prompt for VS 2017**.</span></span> <span data-ttu-id="06de6-229">開發人員命令提示字元在其路徑中會有正確的 *msbuild.exe*，並設定某些 MSBuild 變數。</span><span class="sxs-lookup"><span data-stu-id="06de6-229">The Developer Command Prompt will have the correct *msbuild.exe* in its path and set some MSBuild variables.</span></span>

<span data-ttu-id="06de6-230">MSBuild 使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="06de6-230">MSBuild uses the following syntax:</span></span>

`msbuild <path-to-project-file> /p:DeployOnBuild=true /p:PublishProfile=<Publish Profile>  /p:Username=<USERNAME> /p:Password=<PASSWORD>`

<span data-ttu-id="06de6-231">您可以從 \<發佈名稱>.PublishSettings 檔案取得 `Password`。</span><span class="sxs-lookup"><span data-stu-id="06de6-231">You can get the `Password` from the *\<Publish name>.PublishSettings* file.</span></span> <span data-ttu-id="06de6-232">*.PublishSettings* 檔案可從以下位置下載：</span><span class="sxs-lookup"><span data-stu-id="06de6-232">You can download the *.PublishSettings* file from:</span></span>

- <span data-ttu-id="06de6-233">方案總管：以滑鼠右鍵按一下 Web 應用程式，然後選取 [下載發行設定檔]。</span><span class="sxs-lookup"><span data-stu-id="06de6-233">Solution Explorer: Right click on the Web App and select **Download Publish Profile**.</span></span>
- <span data-ttu-id="06de6-234">Azure 管理入口網站：從 [Web 應用程式] 刀鋒視窗選取 [取得發行設定檔]。</span><span class="sxs-lookup"><span data-stu-id="06de6-234">The Azure Management Portal: Select **Get publish profile** from the  Web App blade.</span></span>

<span data-ttu-id="06de6-235">`Username` 可以在發行設定檔中找到。</span><span class="sxs-lookup"><span data-stu-id="06de6-235">`Username` can be found in the publish profile.</span></span>

<span data-ttu-id="06de6-236">下列範例使用「Web11112 - Web 部署」發行設定檔：</span><span class="sxs-lookup"><span data-stu-id="06de6-236">The following sample uses the "Web11112 - Web Deploy" publish profile:</span></span>

```console
msbuild "C:\Webs\Web1\Web1.csproj" /p:DeployOnBuild=true
 /p:PublishProfile="Web11112 - Web Deploy"  /p:Username="$Web11112"
 /p:Password="<password removed>"
```

## <a name="excluding-files"></a><span data-ttu-id="06de6-237">排除檔案</span><span class="sxs-lookup"><span data-stu-id="06de6-237">Excluding files</span></span>

<span data-ttu-id="06de6-238">發佈 ASP.NET Core Web 應用程式時，會包含 *wwwroot* 資料夾的組建成品和內容。</span><span class="sxs-lookup"><span data-stu-id="06de6-238">When publishing ASP.NET Core web apps, the build artifacts and contents of the *wwwroot* folder are included.</span></span> <span data-ttu-id="06de6-239">`msbuild` 支援[通用慣例模式](https://gruntjs.com/configuring-tasks#globbing-patterns)。</span><span class="sxs-lookup"><span data-stu-id="06de6-239">`msbuild` supports [globbing patterns](https://gruntjs.com/configuring-tasks#globbing-patterns).</span></span> <span data-ttu-id="06de6-240">例如，下列 `<Content>` 項目標記會排除 *wwwroot/content* 資料夾及其所有子資料夾中的所有文字檔 (*.txt*)。</span><span class="sxs-lookup"><span data-stu-id="06de6-240">For example, the following `<Content>` element markup will exclude all text (*.txt*) files from the *wwwroot/content* folder and all its subfolders.</span></span>

```xml
<ItemGroup>
  <Content Update="wwwroot/content/**/*.txt" CopyToPublishDirectory="Never" />
</ItemGroup>
```

<span data-ttu-id="06de6-241">上述標記可以新增至發行設定檔或 *.csproj* 檔案。</span><span class="sxs-lookup"><span data-stu-id="06de6-241">The markup above can be added to a publish profile or the *.csproj* file.</span></span> <span data-ttu-id="06de6-242">當新增至 *.csproj* 檔案時，此規則會新增至專案中的所有發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="06de6-242">When added to the *.csproj* file, the rule is added to all publish profiles in the project.</span></span>

<span data-ttu-id="06de6-243">下列 `<MsDeploySkipRules>` 項目標記會排除 *wwwroot/content* 資料夾中的所有檔案：</span><span class="sxs-lookup"><span data-stu-id="06de6-243">The following `<MsDeploySkipRules>` element markup exludes all files from the *wwwroot/content* folder:</span></span>

```xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFolder">
    <ObjectName>dirPath</ObjectName>
    <AbsolutePath>wwwroot\content</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

<span data-ttu-id="06de6-244">`<MsDeploySkipRules>` 不會刪除部署網站「略過」的目標。</span><span class="sxs-lookup"><span data-stu-id="06de6-244">`<MsDeploySkipRules>`  will not delete the *skip* targets from the deployment site.</span></span> <span data-ttu-id="06de6-245">會從部署網站刪除 `<Content>` 鎖定目標的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="06de6-245">`<Content>` targeted files and folders will be deleted from the deployment site.</span></span> <span data-ttu-id="06de6-246">例如，假設您曾使用下列檔案部署 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="06de6-246">For example, suppose you had deployed a web app with the following files:</span></span>

- <span data-ttu-id="06de6-247">*Views/Home/About1.cshtml*</span><span class="sxs-lookup"><span data-stu-id="06de6-247">*Views/Home/About1.cshtml*</span></span>
- <span data-ttu-id="06de6-248">*Views/Home/About2.cshtml*</span><span class="sxs-lookup"><span data-stu-id="06de6-248">*Views/Home/About2.cshtml*</span></span>
- <span data-ttu-id="06de6-249">*Views/Home/About3.cshtml*</span><span class="sxs-lookup"><span data-stu-id="06de6-249">*Views/Home/About3.cshtml*</span></span>

<span data-ttu-id="06de6-250">如已新增下列 `<MsDeploySkipRules>` 標記，部署網站就不會刪除這些檔案。</span><span class="sxs-lookup"><span data-stu-id="06de6-250">If you added the following `<MsDeploySkipRules>` markup, those files would not be deleted on the deployment site.</span></span>

``` xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About1.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About2.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About3.cshtml</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

<span data-ttu-id="06de6-251">上例中顯示的 `<MsDeploySkipRules>` 標記會防止部署「略過的」檔案，但這些部署一旦部署之後，就不會被刪除。</span><span class="sxs-lookup"><span data-stu-id="06de6-251">The `<MsDeploySkipRules>` markup shown above prevents the *skipped* files from being depoyed, but will not delete those files once they are deployed.</span></span>

<span data-ttu-id="06de6-252">下列 `<Content>` 標記可能會刪除部署網站已鎖定目標的檔案：</span><span class="sxs-lookup"><span data-stu-id="06de6-252">The following `<Content>` markup would delete the targeted files at the deployment site:</span></span>

``` xml
<ItemGroup>
  <Content Update="Views/Home/About?.cshtml" CopyToPublishDirectory="Never" />
</ItemGroup>
```

<span data-ttu-id="06de6-253">使用含上述 `<Content>` 標記的命令列部署，可能會產生類似下面內容的輸出：</span><span class="sxs-lookup"><span data-stu-id="06de6-253">Using command line deployment with the `<Content>` markup above would result in output similar to the following:</span></span>

``` console
MSDeployPublish:
  Starting Web deployment task from source: manifest(C:\Webs\Web1\obj\Release\netcoreapp1.1\PubTmp\Web1.SourceManifest.
  xml) to Destination: auto().
  Deleting file (Web11112\Views\Home\About1.cshtml).
  Deleting file (Web11112\Views\Home\About2.cshtml).
  Deleting file (Web11112\Views\Home\About3.cshtml).
  Updating file (Web11112\web.config).
  Updating file (Web11112\Web1.deps.json).
  Updating file (Web11112\Web1.dll).
  Updating file (Web11112\Web1.pdb).
  Updating file (Web11112\Web1.runtimeconfig.json).
  Successfully executed Web deployment task.
  Publish Succeeded.
Done Building Project "C:\Webs\Web1\Web1.csproj" (default targets).
```

## <a name="including-files"></a><span data-ttu-id="06de6-254">包括檔案</span><span class="sxs-lookup"><span data-stu-id="06de6-254">Including files</span></span>

<span data-ttu-id="06de6-255">下列標記可用來包含發佈網站 *wwwroot/images* 資料夾之專案目錄外的 *images* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="06de6-255">The following markup can be used to include an *images* folder outside the project directory to the *wwwroot/images* folder of the publish site.</span></span>

``` xml
<ItemGroup>
  <_CustomFiles Include="$(MSBuildProjectDirectory)/../images/**/*" />
  <DotnetPublishFiles Include="@(_CustomFiles)">
    <DestinationRelativePath>wwwroot/images/%(RecursiveDir)%(Filename)%(Extension)</DestinationRelativePath>
  </DotnetPublishFiles>
</ItemGroup>
```

<span data-ttu-id="06de6-256">標記可以新增至 *.csproj* 檔案或發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="06de6-256">The markup can be added to the *.csproj* file or the publish profile.</span></span> <span data-ttu-id="06de6-257">如果它新增至 *.csproj* 檔案，會包含在專案的每個發行設定檔中。</span><span class="sxs-lookup"><span data-stu-id="06de6-257">If it's added to the *.csproj* file, it will be included in each publish profile in the project.</span></span>

<span data-ttu-id="06de6-258">下列反白顯示的標記會示範如何：</span><span class="sxs-lookup"><span data-stu-id="06de6-258">The following highlighted markup shows how to:</span></span>

* <span data-ttu-id="06de6-259">將專案外的檔案複製到 *wwwroot* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="06de6-259">Copy a file from outside the project into the *wwwroot* folder.</span></span>
* <span data-ttu-id="06de6-260">排除 *wwwroot\Content* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="06de6-260">Exclude the *wwwroot\Content* folder.</span></span>
* <span data-ttu-id="06de6-261">排除 *Views\Home\About2.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="06de6-261">Exclude *Views\Home\About2.cshtml*.</span></span>

[!code-xml[Main](web-publishing-vs/sample/FolderProfile2.pubxml?highlight=21-29)]

<span data-ttu-id="06de6-262">如需更多的部署範例，請參閱 [WebSDK 讀我檔案](https://github.com/aspnet/websdk)。</span><span class="sxs-lookup"><span data-stu-id="06de6-262">See the [WebSDK Readme](https://github.com/aspnet/websdk) for more deployment samples.</span></span>

### <a name="run-a-target-before-or-after-publishing"></a><span data-ttu-id="06de6-263">在發佈之前或之後執行目標</span><span class="sxs-lookup"><span data-stu-id="06de6-263">Run a target before or after publishing</span></span>

<span data-ttu-id="06de6-264">內建的 `BeforePublish` 和 `AfterPublish` 目標可以用來在發佈目標之前或之後執行目標。</span><span class="sxs-lookup"><span data-stu-id="06de6-264">The builtin `BeforePublish` and `AfterPublish` targets can be used to execute a target before or after the publish target.</span></span> <span data-ttu-id="06de6-265">下列標記可以新增至發行設定檔，先將訊息記錄至主控台輸出再發佈：</span><span class="sxs-lookup"><span data-stu-id="06de6-265">The following markup can be added to the publish profile to log messages to the console output before and after publishing:</span></span>

``` xml
<Target Name="CustomActionsBeforePublish" BeforeTargets="BeforePublish">
    <Message Text="Inside BeforePublish" Importance="high" />
  </Target>
  <Target Name="CustomActionsAfterPublish" AfterTargets="AfterPublish">
    <Message Text="Inside AfterPublish" Importance="high" />
</Target>
```

## <a name="the-kudu-service"></a><span data-ttu-id="06de6-266">Kudu 服務</span><span class="sxs-lookup"><span data-stu-id="06de6-266">The Kudu service</span></span>

<span data-ttu-id="06de6-267">若要檢視 Azure Web 應用程式上的檔案，請使用 [kudu 服務](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service)。</span><span class="sxs-lookup"><span data-stu-id="06de6-267">To view the files on your Azure Web App, use the [kudu service](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service).</span></span> <span data-ttu-id="06de6-268">將 `scm` 權杖附加在名稱或 Web 應用程式之後。</span><span class="sxs-lookup"><span data-stu-id="06de6-268">Append the `scm` token to the name or your Web App.</span></span> <span data-ttu-id="06de6-269">例如: </span><span class="sxs-lookup"><span data-stu-id="06de6-269">For example:</span></span>

| <span data-ttu-id="06de6-270">URL</span><span class="sxs-lookup"><span data-stu-id="06de6-270">URL</span></span>               | <span data-ttu-id="06de6-271">結果</span><span class="sxs-lookup"><span data-stu-id="06de6-271">Result</span></span>|
| ----------------- | ------------ |
| `http://mysite.azurewebsites.net/` | <span data-ttu-id="06de6-272">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="06de6-272">Web App</span></span> |
| `http://mysite.scm.azurewebsites.net/` | <span data-ttu-id="06de6-273">Kudu 服務</span><span class="sxs-lookup"><span data-stu-id="06de6-273">Kudu sevice</span></span> |

<span data-ttu-id="06de6-274">選取[偵錯主控台](https://github.com/projectkudu/kudu/wiki/Kudu-console)功能表項目以檢視/編輯/刪除/新增檔案。</span><span class="sxs-lookup"><span data-stu-id="06de6-274">Select the [Debug Console](https://github.com/projectkudu/kudu/wiki/Kudu-console) menu item to view/edit/delete/add files.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="06de6-275">其他資源</span><span class="sxs-lookup"><span data-stu-id="06de6-275">Additional resources</span></span>

- <span data-ttu-id="06de6-276">[Web 部署](https://www.iis.net/downloads/microsoft/web-deploy) (msdeploy) 可簡化 IIS 伺服器的 Web 應用程式和網站部署。</span><span class="sxs-lookup"><span data-stu-id="06de6-276">[Web Deploy](https://www.iis.net/downloads/microsoft/web-deploy)  (msdeploy) simplifies deployment of Web applications and Web sites to IIS servers.</span></span>

- <span data-ttu-id="06de6-277">[https://github.com/aspnet/websdk](https://github.com/aspnet/websdk/issues)：部署的檔案問題及要求功能。</span><span class="sxs-lookup"><span data-stu-id="06de6-277">[https://github.com/aspnet/websdk](https://github.com/aspnet/websdk/issues): File issues and request features for deployment.</span></span>