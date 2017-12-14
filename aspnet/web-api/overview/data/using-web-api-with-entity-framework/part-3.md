---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: "Use as migrações do Code First para propagar o banco de dados | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: df75a69644033cc76fee86b5a9692ab65beb4d01
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
<a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="4d22e-102">Use as migrações do Code First para propagar o banco de dados</span><span class="sxs-lookup"><span data-stu-id="4d22e-102">Use Code First Migrations to Seed the Database</span></span>
====================
<span data-ttu-id="4d22e-103">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4d22e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="4d22e-104">Baixe o projeto concluído</span><span class="sxs-lookup"><span data-stu-id="4d22e-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="4d22e-105">Nesta seção, você usará [migrações do Code First](https://msdn.microsoft.com/en-us/data/jj591621) no EF para propagar o banco de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="4d22e-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/en-us/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="4d22e-106">Do **ferramentas** menu, selecione **Gerenciador de biblioteca de pacote**, em seguida, selecione **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="4d22e-106">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="4d22e-107">Na janela do Console do Gerenciador de pacotes, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4d22e-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="4d22e-108">Este comando adiciona uma pasta chamada migrações ao seu projeto, além de um arquivo de código chamado Configuration.cs na pasta de migrações.</span><span class="sxs-lookup"><span data-stu-id="4d22e-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="4d22e-109">Abra o arquivo Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="4d22e-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="4d22e-110">Adicione o seguinte **usando** instrução.</span><span class="sxs-lookup"><span data-stu-id="4d22e-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="4d22e-111">Em seguida, adicione o seguinte código para o **Configuration.Seed** método:</span><span class="sxs-lookup"><span data-stu-id="4d22e-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="4d22e-112">Na janela do Console do Gerenciador de pacotes, digite os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4d22e-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="4d22e-113">O primeiro comando gera o código que cria o banco de dados, e o segundo comando executa esse código.</span><span class="sxs-lookup"><span data-stu-id="4d22e-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="4d22e-114">O banco de dados é criado localmente, usando [LocalDB](https://msdn.microsoft.com/en-us/library/hh510202.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d22e-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/en-us/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="4d22e-115">Explorar a API (opcional)</span><span class="sxs-lookup"><span data-stu-id="4d22e-115">Explore the API (Optional)</span></span>

<span data-ttu-id="4d22e-116">Pressione F5 para executar o aplicativo no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="4d22e-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="4d22e-117">O Visual Studio inicia o IIS Express e executa seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="4d22e-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="4d22e-118">Visual Studio, em seguida, inicia um navegador e abre a home page do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4d22e-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="4d22e-119">Quando o Visual Studio executará um projeto da web, ele atribui um número de porta.</span><span class="sxs-lookup"><span data-stu-id="4d22e-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="4d22e-120">Na imagem abaixo, o número da porta é 50524.</span><span class="sxs-lookup"><span data-stu-id="4d22e-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="4d22e-121">Quando você executa o aplicativo, você verá um número de porta diferente.</span><span class="sxs-lookup"><span data-stu-id="4d22e-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="4d22e-122">A home page é implementada usando o ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="4d22e-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="4d22e-123">Na parte superior da página, há um link que diz "API".</span><span class="sxs-lookup"><span data-stu-id="4d22e-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="4d22e-124">Este link traz uma página de ajuda gerada automaticamente para a API da web.</span><span class="sxs-lookup"><span data-stu-id="4d22e-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="4d22e-125">(Para saber como esta página de Ajuda é gerada e como você pode adicionar sua própria documentação para a página, consulte [criando páginas de ajuda para a ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) Você pode clicar no menu Ajuda links da página para ver os detalhes sobre a API, incluindo o formato de solicitação e resposta.</span><span class="sxs-lookup"><span data-stu-id="4d22e-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="4d22e-126">A API permite operações CRUD no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4d22e-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="4d22e-127">A seguir resume a API.</span><span class="sxs-lookup"><span data-stu-id="4d22e-127">The following summarizes the API.</span></span>

| <span data-ttu-id="4d22e-128">Autores</span><span class="sxs-lookup"><span data-stu-id="4d22e-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="4d22e-129">OBTER api/autores</span><span class="sxs-lookup"><span data-stu-id="4d22e-129">GET api/authors</span></span> | <span data-ttu-id="4d22e-130">Obter todos os autores.</span><span class="sxs-lookup"><span data-stu-id="4d22e-130">Get all authors.</span></span> |
| <span data-ttu-id="4d22e-131">Api GET/autores / {id}</span><span class="sxs-lookup"><span data-stu-id="4d22e-131">GET api/authors/{id}</span></span> | <span data-ttu-id="4d22e-132">Obter um autor por ID.</span><span class="sxs-lookup"><span data-stu-id="4d22e-132">Get an author by ID.</span></span> |
| <span data-ttu-id="4d22e-133">Autores/api/POST</span><span class="sxs-lookup"><span data-stu-id="4d22e-133">POST /api/authors</span></span> | <span data-ttu-id="4d22e-134">Crie um novo autor.</span><span class="sxs-lookup"><span data-stu-id="4d22e-134">Create a new author.</span></span> |
| <span data-ttu-id="4d22e-135">COLOCAR /api autores / {id}</span><span class="sxs-lookup"><span data-stu-id="4d22e-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="4d22e-136">Atualize um autor existente.</span><span class="sxs-lookup"><span data-stu-id="4d22e-136">Update an existing author.</span></span> |
| <span data-ttu-id="4d22e-137">Excluir /api autores / {id}</span><span class="sxs-lookup"><span data-stu-id="4d22e-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="4d22e-138">Exclua um autor.</span><span class="sxs-lookup"><span data-stu-id="4d22e-138">Delete an author.</span></span> |

| <span data-ttu-id="4d22e-139">Livros</span><span class="sxs-lookup"><span data-stu-id="4d22e-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="4d22e-140">OBTER /api/books</span><span class="sxs-lookup"><span data-stu-id="4d22e-140">GET /api/books</span></span> | <span data-ttu-id="4d22e-141">Obter todos os livros.</span><span class="sxs-lookup"><span data-stu-id="4d22e-141">Get all books.</span></span> |
| <span data-ttu-id="4d22e-142">OBTER /api manuais / {id}</span><span class="sxs-lookup"><span data-stu-id="4d22e-142">GET /api/books/{id}</span></span> | <span data-ttu-id="4d22e-143">Obter um livro por ID.</span><span class="sxs-lookup"><span data-stu-id="4d22e-143">Get a book by ID.</span></span> |
| <span data-ttu-id="4d22e-144">Enviar/api/catálogos</span><span class="sxs-lookup"><span data-stu-id="4d22e-144">POST /api/books</span></span> | <span data-ttu-id="4d22e-145">Crie um novo catálogo.</span><span class="sxs-lookup"><span data-stu-id="4d22e-145">Create a new book.</span></span> |
| <span data-ttu-id="4d22e-146">COLOCAR /api manuais / {id}</span><span class="sxs-lookup"><span data-stu-id="4d22e-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="4d22e-147">Atualize um catálogo existente.</span><span class="sxs-lookup"><span data-stu-id="4d22e-147">Update an existing book.</span></span> |
| <span data-ttu-id="4d22e-148">Excluir /api manuais / {id}</span><span class="sxs-lookup"><span data-stu-id="4d22e-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="4d22e-149">Exclua um catálogo.</span><span class="sxs-lookup"><span data-stu-id="4d22e-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="4d22e-150">Exibir o banco de dados (opcional)</span><span class="sxs-lookup"><span data-stu-id="4d22e-150">View the Database (Optional)</span></span>

<span data-ttu-id="4d22e-151">Quando você executou o comando Update-Database, EF criou o banco de dados e a chamada a `Seed` método.</span><span class="sxs-lookup"><span data-stu-id="4d22e-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="4d22e-152">Quando você executar o aplicativo localmente, usa EF [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d22e-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="4d22e-153">Você pode exibir o banco de dados no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d22e-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="4d22e-154">Do **exibição** menu, selecione **Pesquisador de objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="4d22e-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="4d22e-155">No **conectar ao servidor** caixa de diálogo, no **nome do servidor** caixa de edição, digite "\v11.0 (localdb)".</span><span class="sxs-lookup"><span data-stu-id="4d22e-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="4d22e-156">Deixe o **autenticação** opção como "Autenticação do Windows".</span><span class="sxs-lookup"><span data-stu-id="4d22e-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="4d22e-157">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="4d22e-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="4d22e-158">Visual Studio se conecta ao LocalDB e mostra os bancos de dados existentes na janela do Pesquisador de objetos do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4d22e-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="4d22e-159">Você pode expandir os nós para ver as tabelas que EF criada.</span><span class="sxs-lookup"><span data-stu-id="4d22e-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="4d22e-160">Para exibir os dados, clique em uma tabela e selecione **exibir dados**.</span><span class="sxs-lookup"><span data-stu-id="4d22e-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="4d22e-161">Captura de tela a seguir mostra os resultados da tabela livros.</span><span class="sxs-lookup"><span data-stu-id="4d22e-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="4d22e-162">Observe que o EF populado o banco de dados com os dados de semente, e a tabela contém a chave estrangeira para a tabela de autores.</span><span class="sxs-lookup"><span data-stu-id="4d22e-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

>[!div class="step-by-step"]
<span data-ttu-id="4d22e-163">[Anterior](part-2.md)
[Próximo](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="4d22e-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>