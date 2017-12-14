---
uid: web-api/overview/security/forms-authentication
title: "Autenticação de formulários ASP.NET Web API | Microsoft Docs"
author: MikeWasson
description: "Descreve como usar a autenticação de formulários na API da Web do ASP.NET."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 9027d76bcf8854fc85f11906d3651511f350cd32
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
<a name="forms-authentication-in-aspnet-web-api"></a><span data-ttu-id="2de9a-103">Autenticação de formulários na API da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2de9a-103">Forms Authentication in ASP.NET Web API</span></span>
====================
<span data-ttu-id="2de9a-104">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2de9a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2de9a-105">Autenticação de formulários usa um formulário HTML para enviar as credenciais do usuário para o servidor.</span><span class="sxs-lookup"><span data-stu-id="2de9a-105">Forms authentication uses an HTML form to send the user's credentials to the server.</span></span> <span data-ttu-id="2de9a-106">Não é um padrão da Internet.</span><span class="sxs-lookup"><span data-stu-id="2de9a-106">It is not an Internet standard.</span></span> <span data-ttu-id="2de9a-107">Autenticação de formulários só é adequada para APIs da web que são chamados de um aplicativo web, para que o usuário pode interagir com o formulário HTML.</span><span class="sxs-lookup"><span data-stu-id="2de9a-107">Forms authentication is only appropriate for web APIs that are called from a web application, so that the user can interact with the HTML form.</span></span>

| <span data-ttu-id="2de9a-108">Vantagens</span><span class="sxs-lookup"><span data-stu-id="2de9a-108">Advantages</span></span> | <span data-ttu-id="2de9a-109">Desvantagens</span><span class="sxs-lookup"><span data-stu-id="2de9a-109">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="2de9a-110">-Fácil de implementar: internos do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2de9a-110">- Easy to implement: Built into ASP.NET.</span></span> <span data-ttu-id="2de9a-111">-Usa o provedor de associação do ASP.NET, o que torna mais fácil gerenciar contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="2de9a-111">- Uses ASP.NET membership provider, which makes it easy to manage user accounts.</span></span> | <span data-ttu-id="2de9a-112">-Não um padrão mecanismo de autenticação HTTP; usa cookies HTTP em vez de cabeçalho de autorização padrão.</span><span class="sxs-lookup"><span data-stu-id="2de9a-112">- Not a standard HTTP authentication mechanism; uses HTTP cookies instead of the standard Authorization header.</span></span> <span data-ttu-id="2de9a-113">-Requer um cliente de navegador.</span><span class="sxs-lookup"><span data-stu-id="2de9a-113">- Requires a browser client.</span></span> <span data-ttu-id="2de9a-114">-Credenciais são enviadas como texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="2de9a-114">- Credentials are sent as plaintext.</span></span> <span data-ttu-id="2de9a-115">-Vulnerável a falsificação de solicitação entre sites (CSRF); requer medidas anti-CSRF.</span><span class="sxs-lookup"><span data-stu-id="2de9a-115">- Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span> <span data-ttu-id="2de9a-116">-Difícil de usar de nonbrowser clientes.</span><span class="sxs-lookup"><span data-stu-id="2de9a-116">- Difficult to use from nonbrowser clients.</span></span> <span data-ttu-id="2de9a-117">Logon requer um navegador.</span><span class="sxs-lookup"><span data-stu-id="2de9a-117">Login requires a browser.</span></span> <span data-ttu-id="2de9a-118">-As credenciais do usuário são enviadas na solicitação.</span><span class="sxs-lookup"><span data-stu-id="2de9a-118">- User credentials are sent in the request.</span></span> <span data-ttu-id="2de9a-119">-Alguns usuários desabilitam cookies.</span><span class="sxs-lookup"><span data-stu-id="2de9a-119">- Some users disable cookies.</span></span> |

<span data-ttu-id="2de9a-120">Em resumo, a autenticação de formulários do ASP.NET funciona da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="2de9a-120">Briefly, forms authentication in ASP.NET works like this:</span></span>

1. <span data-ttu-id="2de9a-121">O cliente solicita um recurso que exige autenticação.</span><span class="sxs-lookup"><span data-stu-id="2de9a-121">The client requests a resource that requires authentication.</span></span>
2. <span data-ttu-id="2de9a-122">Se o usuário não é autenticado, o servidor retorna HTTP 302 (não encontrado) e redireciona para uma página de logon.</span><span class="sxs-lookup"><span data-stu-id="2de9a-122">If the user is not authenticated, the server returns HTTP 302 (Found) and redirects to a login page.</span></span>
3. <span data-ttu-id="2de9a-123">O usuário insere as credenciais e envia o formulário.</span><span class="sxs-lookup"><span data-stu-id="2de9a-123">The user enters credentials and submits the form.</span></span>
4. <span data-ttu-id="2de9a-124">O servidor retorna outro HTTP 302 redireciona de volta para o URI original.</span><span class="sxs-lookup"><span data-stu-id="2de9a-124">The server returns another HTTP 302 that redirects back to the original URI.</span></span> <span data-ttu-id="2de9a-125">Essa resposta inclui um cookie de autenticação.</span><span class="sxs-lookup"><span data-stu-id="2de9a-125">This response includes an authentication cookie.</span></span>
5. <span data-ttu-id="2de9a-126">O cliente solicita o recurso novamente.</span><span class="sxs-lookup"><span data-stu-id="2de9a-126">The client requests the resource again.</span></span> <span data-ttu-id="2de9a-127">A solicitação inclui o cookie de autenticação para que o servidor concede a solicitação.</span><span class="sxs-lookup"><span data-stu-id="2de9a-127">The request includes the authentication cookie, so the server grants the request.</span></span>

![](forms-authentication/_static/image1.png)

<span data-ttu-id="2de9a-128">Para obter mais informações, consulte [uma visão geral de formulários de autenticação.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span><span class="sxs-lookup"><span data-stu-id="2de9a-128">For more information, see [An Overview of Forms Authentication.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span></span>

## <a name="using-forms-authentication-with-web-api"></a><span data-ttu-id="2de9a-129">Usando a autenticação de formulários com a API da Web</span><span class="sxs-lookup"><span data-stu-id="2de9a-129">Using Forms Authentication with Web API</span></span>

<span data-ttu-id="2de9a-130">Para criar um aplicativo que usa autenticação de formulários, selecione o modelo de "Aplicativo de Internet" no Assistente de projeto MVC 4.</span><span class="sxs-lookup"><span data-stu-id="2de9a-130">To create an application that uses forms authentication, select the "Internet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="2de9a-131">Este modelo cria controladores MVC para gerenciamento de conta.</span><span class="sxs-lookup"><span data-stu-id="2de9a-131">This template creates MVC controllers for account management.</span></span> <span data-ttu-id="2de9a-132">Você também pode usar o modelo de "Aplicativo de página única", disponível no ASP.NET estão 2012 Update.</span><span class="sxs-lookup"><span data-stu-id="2de9a-132">You can also use the "Single Page Application" template, available in the ASP.NET Fall 2012 Update.</span></span>

<span data-ttu-id="2de9a-133">Em seus controladores de API da web, você pode restringir o acesso por meio de `[Authorize]` de atributo, conforme descrito em [usando o atributo [autorizar]](authentication-and-authorization-in-aspnet-web-api.md#auth3).</span><span class="sxs-lookup"><span data-stu-id="2de9a-133">In your web API controllers, you can restrict access by using the `[Authorize]` attribute, as described in [Using the [Authorize] Attribute](authentication-and-authorization-in-aspnet-web-api.md#auth3).</span></span>

<span data-ttu-id="2de9a-134">Autenticação de formulários usa um cookie de sessão para autenticar solicitações.</span><span class="sxs-lookup"><span data-stu-id="2de9a-134">Forms-authentication uses a session cookie to authenticate requests.</span></span> <span data-ttu-id="2de9a-135">Navegadores enviam automaticamente todos os cookies relevantes para o site de destino.</span><span class="sxs-lookup"><span data-stu-id="2de9a-135">Browsers automatically send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="2de9a-136">Esse recurso facilita a autenticação de formulários vulnerável a ver os ataques CSRF (falsificação) de solicitação intersite [ataques de falsificação de solicitação intersite impedindo (CSRF)](preventing-cross-site-request-forgery-csrf-attacks.md).</span><span class="sxs-lookup"><span data-stu-id="2de9a-136">This feature makes forms authentication potentially vulnerable to cross-site request forgery (CSRF) attacks See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="2de9a-137">Autenticação de formulários não criptografa as credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="2de9a-137">Forms authentication does not encrypt the user's credentials.</span></span> <span data-ttu-id="2de9a-138">Portanto, a autenticação de formulários não é segura, a menos que usado com SSL.</span><span class="sxs-lookup"><span data-stu-id="2de9a-138">Therefore, forms authentication is not secure unless used with SSL.</span></span> <span data-ttu-id="2de9a-139">Consulte [trabalhar com SSL na API da Web](working-with-ssl-in-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="2de9a-139">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>