---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: Ajustando o índice Z de uma sombra (VB) | Microsoft Docs
author: wenz
description: O controle de sombra no AJAX Control Toolkit estende um painel com uma sombra. No entanto essa sombra às vezes, está em conflito com outros controles, para insta...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: b484dc6bfa6f67bd6b70f7c36c2eb2ec7143edaf
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
<a name="adjusting-the-z-index-of-a-dropshadow-vb"></a>Ajustando o índice Z de uma sombra (VB)
====================
por [Christian Wenz](https://github.com/wenz)

[Baixar o código](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)

> O controle de sombra no AJAX Control Toolkit estende um painel com uma sombra. No entanto essa sombra às vezes, está em conflito com outros controles, por exemplo, o controle de Menu do ASP.NET. Quando uma entrada de menu é exibido, ele aparece atrás a sombra projetada.


## <a name="overview"></a>Visão geral

O controle de sombra no AJAX Control Toolkit estende um painel com uma sombra. No entanto essa sombra às vezes, está em conflito com outros controles, por exemplo, o controle de Menu do ASP.NET. Quando uma entrada de menu é exibido, ele aparece atrás a sombra projetada.

## <a name="steps"></a>Etapas

O código começa com o próprio painel, que contém texto suficiente para que o painel contém texto suficiente para que o efeito seja visível:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

Outro painel é colocado diretamente antes do `panelShadow` painel. Ele contém um menu com orientação horizontal para que as entradas do menu exibido acima (ou ainda: sob) o `dropShadow` painel):

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

Em seguida, o `DropShadowExtender` é adicionado ao estender o `panelShadow` painel com um efeito de sombra:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

Por fim, o ASP.NET AJAX `ScriptManager` controle permite que o Kit de ferramentas de controle funcionar:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

Quando você executar esse script, as entradas do menu aparecem sob o painel. No entanto, o menu usa a classe CSS `panel` onde você só precisa definir duas coisas para fazer com que elementos exibidos na frente do painel de:

- Posicionamento relativo
- Um índice z positivo

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

Em seguida, o `DropShadowExtender` controle não está em conflito mais com o controle de Menu.


[![Antes: A entrada de menu não está visível](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)

Antes: A entrada de menu não estiver visível ([clique para exibir a imagem em tamanho normal](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))


[![Depois: A entrada de menu é exibido](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)

Depois: A entrada de menu é exibido ([clique para exibir a imagem em tamanho normal](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))

> [!div class="step-by-step"]
> [Anterior](manipulating-dropshadow-properties-from-client-code-cs.md)
> [Próximo](manipulating-dropshadow-properties-from-client-code-vb.md)
