---
title: "Desenvolvendo aplicativos ASP.NET Core usando a inspeção dotnet"
author: rick-anderson
description: Este tutorial demonstra como instalar e usar a ferramenta de inspetor de arquivo (dotnet watch) da CLI do .NET Core em um aplicativo do ASP.NET Core.
manager: wpickett
ms.author: riande
ms.date: 10/05/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: tutorials/dotnet-watch
ms.openlocfilehash: cb15e28cb98ea82091cf5ddeed12df8926079e52
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2018
---
# <a name="developing-aspnet-core-apps-using-dotnet-watch"></a>Desenvolvendo aplicativos ASP.NET Core usando a inspeção dotnet

Por [Rick Anderson](https://twitter.com/RickAndMSFT) e [Victor Hurdugaci](https://twitter.com/victorhurdugaci)

`dotnet watch` é uma ferramenta que executa um comando do [CLI do .NET Core](/dotnet/core/tools) quando os arquivos de origem são alterados. Por exemplo, uma alteração de arquivo pode disparar uma compilação, execução de teste ou uma implantação.

Neste tutorial, usamos um aplicativo de API Web existente com dois pontos de extremidade: um que retorna uma soma e outro que retorna um produto. O método de produto contém um bug que corrigiremos como parte deste tutorial.

Baixe o [aplicativo de exemplo](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/dotnet-watch/sample). Ele contém dois projetos: *WebApp* (uma API do ASP.NET Core Web) e *WebAppTests* (testes de unidade para a API da Web).

Em um shell de comando, navegue para a pasta *WebApp* e execute os seguintes comandos:

```console
dotnet run
```

O resultado do console mostra mensagens semelhantes à seguinte (indicando que o aplicativo está em execução e aguarda solicitações):

```console
$ dotnet run
Hosting environment: Development
Content root path: C:/Docs/aspnetcore/tutorials/dotnet-watch/sample/WebApp
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

Em um navegador da Web, navegue até `http://localhost:<port number>/api/math/sum?a=4&b=5`. Você deve ver o resultado de `9`.

Navegue para o API do produto (`http://localhost:<port number>/api/math/product?a=4&b=5`). Ele retorna `9`, não `20`, conforme o esperado. Corrigiremos isso mais adiante no tutorial.

## <a name="add-dotnet-watch-to-a-project"></a>Adicionar `dotnet watch` a um projeto

1. Adicionar uma referência ao pacote de `Microsoft.DotNet.Watcher.Tools` para o arquivo *.csproj*:

    ```xml
    <ItemGroup>
        <DotNetCliToolReference Include="Microsoft.DotNet.Watcher.Tools" Version="2.0.0" />
    </ItemGroup> 
    ```

1. Instale o pacote `Microsoft.DotNet.Watcher.Tools` executando o seguinte comando:
    
    ```console
    dotnet restore
    ```

## <a name="running-net-core-cli-commands-using-dotnet-watch"></a>Executando comandos da CLI do .NET Core usando `dotnet watch`

Qualquer [comando da CLI do .NET Core](/dotnet/core/tools#cli-commands) pode ser executado com `dotnet watch`. Por exemplo:

| Comando | Comando com inspeção |
| ---- | ----- |
| dotnet run | dotnet watch run |
| dotnet run -f netcoreapp2.0 | dotnet watch run -f netcoreapp2.0 |
| dotnet run -f netcoreapp2.0 -- --arg1 | dotnet watch run -f netcoreapp2.0 -- --arg1 |
| dotnet test | dotnet watch test |

Executar `dotnet watch run` na pasta *WebApp*. O resultado do console indica que `watch` foi iniciado.

## <a name="making-changes-with-dotnet-watch"></a>Fazer alterações com `dotnet watch`

Verifique se `dotnet watch` está em execução.

Corrija o bug no método `Product` do *MathController.cs* para que ele retorne o produto e não a soma:

```csharp
public static int Product(int a, int b)
{
  return a * b;
} 
```

Salve o arquivo. O resultado do console indica que o `dotnet watch` detectou uma alteração de arquivo e reiniciou o aplicativo.

Verifique se `http://localhost:<port number>/api/math/product?a=4&b=5` retorna o resultado correto.

## <a name="running-tests-using-dotnet-watch"></a>Executando testes usando `dotnet watch`

1. Altere o método `Product` de *MathController.cs* novamente para retornar a soma e salve o arquivo.
1. Em um shell de comando, navegue até a pasta *WebAppTests*.
1. Execute `dotnet restore`.
1. Execute `dotnet watch test`. Seu resultado indica que um teste falhou e que o inspetor está aguardando as alterações de arquivo:

     ```console
     Total tests: 2. Passed: 1. Failed: 1. Skipped: 0.
     Test Run Failed.
     ```

1. Corrija o código do método `Product` para que ele retorne o produto. Salve o arquivo.

`dotnet watch` detecta a alteração de arquivo e executa os testes novamente. O resultado do console indica a aprovação nos testes.

## <a name="dotnet-watch-in-github"></a>dotnet-watch no GitHub

dotnet-watch faz parte do [repositório DotNetTools](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-watch) do GitHub.

A [seção MSBuild](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-watch#msbuild) do [Leiame do dotnet-watch](https://github.com/aspnet/DotNetTools/blob/dev/src/dotnet-watch/README.md) explica como o dotnet-watch pode ser configurado por meio do arquivo de projeto MSBuild inspecionado. O [Leiame do dotnet-watch](https://github.com/aspnet/DotNetTools/blob/dev/src/dotnet-watch/README.md) contém informações sobre o dotnet-watch não abordadas neste tutorial.
