---
uid: signalr/overview/releases/upgrading-signalr-1x-projects-to-20
title: "Atualizando projetos do SignalR 1. x para a versão 2 | Microsoft Docs"
author: pfletcher
description: "Este tópico descreve como atualizar um projeto existente de 1. x do SignalR para SignalR 2. x e como solucionar problemas que podem surgir durante o processo de atualização..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: adcfef99-9bc5-489d-a91b-9b7c2bc35e04
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/releases/upgrading-signalr-1x-projects-to-20
msc.type: authoredcontent
ms.openlocfilehash: e372275ae5dd4bbf354db2d02e4407f8c513b7a3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
<a name="upgrading-signalr-1x-projects-to-version-2"></a><span data-ttu-id="8a88e-103">Atualizando projetos do SignalR 1. x para a versão 2</span><span class="sxs-lookup"><span data-stu-id="8a88e-103">Upgrading SignalR 1.x Projects to version 2</span></span>
====================
<span data-ttu-id="8a88e-104">por [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="8a88e-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="8a88e-105">Este tópico descreve como atualizar um projeto existente de 1. x do SignalR para SignalR 2. x e como solucionar problemas que podem surgir durante o processo de atualização.</span><span class="sxs-lookup"><span data-stu-id="8a88e-105">This topic describes how to upgrade an existing SignalR 1.x project to SignalR 2.x, and how to troubleshoot issues that may arise during the upgrade process.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8a88e-106">Versões de software usadas no tutorial</span><span class="sxs-lookup"><span data-stu-id="8a88e-106">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="8a88e-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="8a88e-107">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="8a88e-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="8a88e-108">.NET 4.5</span></span>
> - <span data-ttu-id="8a88e-109">Versões 1 e 2 do SignalR</span><span class="sxs-lookup"><span data-stu-id="8a88e-109">SignalR versions 1 and 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="8a88e-110">Usando o Visual Studio 2012 com este tutorial</span><span class="sxs-lookup"><span data-stu-id="8a88e-110">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="8a88e-111">Para usar o Visual Studio 2012 com este tutorial, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8a88e-111">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="8a88e-112">Atualização de seu [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="8a88e-112">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="8a88e-113">Instalar o [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a88e-113">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="8a88e-114">No Web Platform Installer, procurar e instalar **ASP.NET e Web 2013.1 de ferramentas para Visual Studio 2012**.</span><span class="sxs-lookup"><span data-stu-id="8a88e-114">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="8a88e-115">Isso irá instalar os modelos do Visual Studio para SignalR classes como **Hub**.</span><span class="sxs-lookup"><span data-stu-id="8a88e-115">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="8a88e-116">Alguns modelos (como **classe de inicialização OWIN**) não estará disponível; para isso, use um arquivo de classe em vez disso.</span><span class="sxs-lookup"><span data-stu-id="8a88e-116">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="8a88e-117">Perguntas e comentários</span><span class="sxs-lookup"><span data-stu-id="8a88e-117">Questions and comments</span></span>
> 
> <span data-ttu-id="8a88e-118">Deixe comentários em como você gostou neste tutorial e o que podemos melhorar nos comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="8a88e-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="8a88e-119">Se você tiver dúvidas que não estão diretamente relacionadas ao tutorial, você poderá postá-los para o [ASP.NET SignalR fórum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="8a88e-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="8a88e-120">SignalR 2 oferece uma experiência de desenvolvimento consistente entre as plataformas de servidor usando [OWIN](http://owin.org).</span><span class="sxs-lookup"><span data-stu-id="8a88e-120">SignalR 2 offers a consistent development experience across server platforms using [OWIN](http://owin.org).</span></span> <span data-ttu-id="8a88e-121">Este artigo descreve as etapas necessárias para atualizar um aplicativo de 1. x SignalR para a versão 2.</span><span class="sxs-lookup"><span data-stu-id="8a88e-121">This article describes the few steps that are needed to update a SignalR 1.x application to version 2.</span></span>

<span data-ttu-id="8a88e-122">Enquanto ele é recomendável atualizar aplicativos para 2 SignalR, SignalR 1. x ainda suporte.</span><span class="sxs-lookup"><span data-stu-id="8a88e-122">While it is encouraged to upgrade applications to SignalR 2, SignalR 1.x will still be supported.</span></span>

<span data-ttu-id="8a88e-123">Este tutorial descreve como atualizar um aplicativo web hospedado para o SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="8a88e-123">This tutorial describes how to upgrade a web-hosted application to SignalR 2.</span></span> <span data-ttu-id="8a88e-124">Agora há suporte para aplicativos de hospedagem interna (aquelas que hospedam um servidor em um aplicativo de console, o serviço do Windows ou outro processo) em 2 de SignalR.</span><span class="sxs-lookup"><span data-stu-id="8a88e-124">Self-hosted applications (those that host a server in a console application, Windows service, or other process) are now supported under SignalR 2.</span></span> <span data-ttu-id="8a88e-125">Para obter informações sobre como começar a criar um aplicativo hospedado automaticamente com o SignalR 2, consulte [Tutorial: SignalR auto-host](../deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="8a88e-125">For information on how to get started creating a self-hosted application with SignalR 2, see [Tutorial: SignalR Self-Host](../deployment/tutorial-signalr-self-host.md).</span></span>

## <a name="contents"></a><span data-ttu-id="8a88e-126">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="8a88e-126">Contents</span></span>

<span data-ttu-id="8a88e-127">As seções a seguir descrevem as tarefas envolvidas na atualização de projetos de SignalR e como solucionar problemas que podem surgir.</span><span class="sxs-lookup"><span data-stu-id="8a88e-127">The following sections describe tasks involved with upgrading SignalR projects, and how to troubleshoot issues that may arise.</span></span>

- [<span data-ttu-id="8a88e-128">Exemplo: Atualizar o tutorial de Introdução para o SignalR 2</span><span class="sxs-lookup"><span data-stu-id="8a88e-128">Example: Upgrading the Getting Started tutorial to SignalR 2</span></span>](#example)
- [<span data-ttu-id="8a88e-129">Solucionando problemas de erros encontrados durante a atualização</span><span class="sxs-lookup"><span data-stu-id="8a88e-129">Troubleshooting errors encountered during upgrading</span></span>](#troubleshooting)

<a id="example"></a>

## <a name="example-upgrading-the-getting-started-tutorial-application-to-signalr-2"></a><span data-ttu-id="8a88e-130">Exemplo: Atualizar o aplicativo tutorial de Introdução para SignalR 2</span><span class="sxs-lookup"><span data-stu-id="8a88e-130">Example: Upgrading the Getting Started tutorial application to SignalR 2</span></span>

<span data-ttu-id="8a88e-131">Nesta seção, você atualizará o aplicativo criado no [SignalR versão 1. x do Tutorial de Introdução](../older-versions/index.md) usar 2 SignalR.</span><span class="sxs-lookup"><span data-stu-id="8a88e-131">In this section, you'll update the application created in the [SignalR 1.x version of the Getting Started Tutorial](../older-versions/index.md) to use SignalR 2.</span></span>

1. <span data-ttu-id="8a88e-132">Depois de concluir o tutorial de Introdução, clique com botão direito no projeto e selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="8a88e-132">Once you've finished the Getting Started tutorial, right-click on the project, and select **Properties**.</span></span> <span data-ttu-id="8a88e-133">Verifique o **framework de destino** é definido como **.NET Framework 4.5.**</span><span class="sxs-lookup"><span data-stu-id="8a88e-133">Verify that the **Target framework** is set to **.NET Framework 4.5.**</span></span>
2. <span data-ttu-id="8a88e-134">Abra o Console do Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="8a88e-134">Open the Package Manager Console.</span></span> <span data-ttu-id="8a88e-135">Remover SignalR 1. x do projeto usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8a88e-135">Remove SignalR 1.x from the project using the following command:</span></span>

    [!code-powershell[Main](upgrading-signalr-1x-projects-to-20/samples/sample1.ps1)]
3. <span data-ttu-id="8a88e-136">Instale o SignalR 2 usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8a88e-136">Install SignalR 2 using the following command:</span></span>

    [!code-powershell[Main](upgrading-signalr-1x-projects-to-20/samples/sample2.ps1)]
4. <span data-ttu-id="8a88e-137">Na página HTML, atualize a referência de script para o SignalR corresponder à versão do script agora está incluído no projeto.</span><span class="sxs-lookup"><span data-stu-id="8a88e-137">In the HTML page, update the script reference for SignalR to match the version of the script now included in the project.</span></span>

    [!code-html[Main](upgrading-signalr-1x-projects-to-20/samples/sample3.html)]
5. <span data-ttu-id="8a88e-138">Na classe de aplicativo global, remova a chamada para MapHubs.</span><span class="sxs-lookup"><span data-stu-id="8a88e-138">In the global application class, remove the call to MapHubs.</span></span>

    [!code-csharp[Main](upgrading-signalr-1x-projects-to-20/samples/sample4.cs)]
6. <span data-ttu-id="8a88e-139">A solução e selecione **adicionar**, **Novo Item...** . Na caixa de diálogo, selecione **classe de inicialização Owin**.</span><span class="sxs-lookup"><span data-stu-id="8a88e-139">Right-click the solution, and select **Add**, **New Item...**. In the dialog, select **Owin Startup Class**.</span></span> <span data-ttu-id="8a88e-140">Nomeie a nova classe **Startup.cs**.</span><span class="sxs-lookup"><span data-stu-id="8a88e-140">Name the new class **Startup.cs**.</span></span>

    ![](upgrading-signalr-1x-projects-to-20/_static/image1.png)
7. <span data-ttu-id="8a88e-141">Substitua o conteúdo do Startup.cs com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="8a88e-141">Replace the contents of Startup.cs with the following code:</span></span>

    [!code-csharp[Main](upgrading-signalr-1x-projects-to-20/samples/sample5.cs)]

    <span data-ttu-id="8a88e-142">O atributo do assembly adiciona a classe para o processo de inicialização do Owin, que executa o `Configuration` método quando Owin é iniciado.</span><span class="sxs-lookup"><span data-stu-id="8a88e-142">The assembly attribute adds the class to Owin's startup process, which executes the `Configuration` method when Owin starts up.</span></span> <span data-ttu-id="8a88e-143">Por sua vez chama o `MapSignalR` método, que cria rotas para todos os hubs de SignalR no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8a88e-143">This in turn calls the `MapSignalR` method, which creates routes for all SignalR hubs in the application.</span></span>
8. <span data-ttu-id="8a88e-144">Execute o projeto e copie a URL da página principal para outro navegador ou no painel do navegador, como antes.</span><span class="sxs-lookup"><span data-stu-id="8a88e-144">Run the project, and copy the URL of the main page into another browser or browser pane, as before.</span></span> <span data-ttu-id="8a88e-145">Cada página solicitará um nome de usuário e as mensagens enviadas de cada página devem estar visíveis em ambos os painéis do navegador.</span><span class="sxs-lookup"><span data-stu-id="8a88e-145">Each page will ask for a username, and messages sent from each page should be visible in both browser panes.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting-errors-encountered-during-upgrading"></a><span data-ttu-id="8a88e-146">Solucionando problemas de erros encontrados durante a atualização</span><span class="sxs-lookup"><span data-stu-id="8a88e-146">Troubleshooting errors encountered during upgrading</span></span>

<span data-ttu-id="8a88e-147">Esta seção descreve problemas que podem surgir durante a atualização.</span><span class="sxs-lookup"><span data-stu-id="8a88e-147">This section describes issues that may arise during upgrading.</span></span> <span data-ttu-id="8a88e-148">Para obter uma lista mais completa de erros e problemas que podem ocorrer com um aplicativo SignalR, consulte [solução de problemas do SignalR](../testing-and-debugging/troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8a88e-148">For a more comprehensive list of errors and issues that may occur with a SignalR application, see [SignalR Troubleshooting](../testing-and-debugging/troubleshooting.md).</span></span>

### <a name="the-call-is-ambiguous-between-the-following-methods-or-properties"></a><span data-ttu-id="8a88e-149">'A chamada é ambígua entre os seguintes métodos ou propriedades'</span><span class="sxs-lookup"><span data-stu-id="8a88e-149">'The call is ambiguous between the following methods or properties'</span></span>

<span data-ttu-id="8a88e-150">Este erro ocorrerá se uma referência a `Microsoft.AspNet.SignalR.Owin` não é removido.</span><span class="sxs-lookup"><span data-stu-id="8a88e-150">This error will occur if a reference to `Microsoft.AspNet.SignalR.Owin` is not removed.</span></span> <span data-ttu-id="8a88e-151">Este pacote é substituído; a referência deve ser removida e a versão 1. x do pacote SelfHost deve ser desinstalada.</span><span class="sxs-lookup"><span data-stu-id="8a88e-151">This package is deprecated; the reference must be removed and the 1.x version of the SelfHost package must be uninstalled.</span></span>

### <a name="hub-methods-fail-silently"></a><span data-ttu-id="8a88e-152">Métodos de Hub falharem em modo silencioso</span><span class="sxs-lookup"><span data-stu-id="8a88e-152">Hub methods fail silently</span></span>

<span data-ttu-id="8a88e-153">Verifique se as referências de script no seu cliente até a data e que o `OwinStartup` atributo para sua classe de inicialização tem a classe correta e nomes de assembly para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="8a88e-153">Verify that the script references in your client are up to date, and that the `OwinStartup` attribute for your Startup class has the correct class and assembly names for your project.</span></span> <span data-ttu-id="8a88e-154">Além disso, tente abrir o endereço de hubs (hubs de signalr /) em seu navegador; qualquer erro que aparece oferecem mais informações sobre o que está acontecendo errado.</span><span class="sxs-lookup"><span data-stu-id="8a88e-154">Also, try opening up the hubs address (/signalr/hubs) in your browser; any error that appears will offer more information about what's going wrong.</span></span>