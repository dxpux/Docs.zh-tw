<span data-ttu-id="74cff-101">由 [Rick Anderson](https://twitter.com/RickAndMSFT) 提供</span><span class="sxs-lookup"><span data-stu-id="74cff-101">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="74cff-102">在本節中，您可以新增類別來管理資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="74cff-102">In this section, you add classes for managing movies in a database.</span></span> <span data-ttu-id="74cff-103">搭配 [Entity Framework Core](https://docs.microsoft.com/ef/core) (EF Core) 使用這些類別，即可使用資料庫。</span><span class="sxs-lookup"><span data-stu-id="74cff-103">You use these classes with [Entity Framework Core](https://docs.microsoft.com/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="74cff-104">EF Core 是一種物件關聯式對應 (ORM) 架構，可簡化您必須撰寫的資料存取程式碼。</span><span class="sxs-lookup"><span data-stu-id="74cff-104">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span>

<span data-ttu-id="74cff-105">您所建立的模型類別稱為 POCO 類別 (來自「純舊 CLR 物件」)，因為它們對 EF Core 沒有任何相依性。</span><span class="sxs-lookup"><span data-stu-id="74cff-105">The model classes you create are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="74cff-106">它們會定義資料儲存在資料庫中的屬性。</span><span class="sxs-lookup"><span data-stu-id="74cff-106">They define the properties of the data that are stored in the database.</span></span>

<span data-ttu-id="74cff-107">在本教學課程中，您首先要撰寫模型類別，而 EF Core 會建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="74cff-107">In this tutorial, you write the model classes first, and EF Core creates the database.</span></span> <span data-ttu-id="74cff-108">本文未提及的替代方法是[從現有的資料庫產生模型類別](https://docs.microsoft.com/ef/core/get-started/aspnetcore/existing-db)。</span><span class="sxs-lookup"><span data-stu-id="74cff-108">An alternate approach not covered here is to [generate model classes from an existing database](https://docs.microsoft.com/ef/core/get-started/aspnetcore/existing-db).</span></span>

<span data-ttu-id="74cff-109">[檢視或下載](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie)範例。</span><span class="sxs-lookup"><span data-stu-id="74cff-109">[View or download](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) sample.</span></span>