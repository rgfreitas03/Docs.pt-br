---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: Abrindo uma janela pop-up Modal do código do servidor (c#) | Microsoft Docs
author: wenz
description: O controle ModalPopup no Kit de ferramentas de controle AJAX oferece uma maneira simples para criar um pop-up modal usando meios do lado do cliente. No entanto, alguns cenários exigem que o...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 04bb056ee29065a472a70d480568b897a789ae59
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
<a name="launching-a-modal-popup-window-from-server-code-c"></a>Abrindo uma janela pop-up Modal do código do servidor (c#)
====================
por [Christian Wenz](https://github.com/wenz)

[Baixar o código](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)

> O controle ModalPopup no Kit de ferramentas de controle AJAX oferece uma maneira simples para criar um pop-up modal usando meios do lado do cliente. No entanto, alguns cenários exigem que a abertura do popup modal é acionada no lado do servidor.


## <a name="overview"></a>Visão geral

O controle ModalPopup no Kit de ferramentas de controle AJAX oferece uma maneira simples para criar um pop-up modal usando meios do lado do cliente. No entanto, alguns cenários exigem que a abertura do popup modal é acionada no lado do servidor.

## <a name="steps"></a>Etapas

Em primeiro lugar, um controle de botão do ASP.NET web é necessário para demonstrar como funciona o controle ModalPopup. Adicionar um botão desse tipo dentro de &lt;formulário&gt; elemento em uma nova página:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

Em seguida, você precisa a marcação para o pop-up que você deseja criar. Defina-o como um `<asp:Panel>` de controle e certifique-se de que ele inclui um controle de botão. O controle ModalPopup oferece a funcionalidade para tornar este botão fechar o janela pop-up; Caso contrário, não há nenhuma maneira fácil de deixá-lo desaparecer.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

Em seguida adicione o controle ModalPopup do Kit de ferramentas do ASP.NET AJAX para a página. Definir propriedades para o botão que carrega o controle, o botão que torna desaparecem e a ID de pop-up do real.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

Assim como acontece com todas as páginas da web com base no ASP.NET AJAX; o Gerenciador de Script é necessário para carregar as bibliotecas JavaScript necessárias para os navegadores de destino diferente:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

Execute o exemplo no navegador. Quando você clica no botão, aparece o pop-up modal. Para obter o mesmo efeito que usar o código do lado do servidor, é necessário um novo botão:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

Como você pode ver, um clique no botão gera um postback e executa o `ServerButton_Click()` método no servidor. Esse método, uma função JavaScript chamada `launchModal()` é executado para ser exata, a função JavaScript será executada depois que a página foi carregada:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

O trabalho de `launchModal()` é exibir o ModalPopup. O `launchModal()` função é executada depois que a página HTML completa foi carregada. No momento, no entanto, a estrutura do ASP.NET AJAX não foi totalmente carregada ainda. Portanto, o `launchModal()` função define apenas uma variável que o controle ModalPopup deve ser mostrado posteriormente:

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

O `pageLoad()` JavaScript é uma função especial que é executada depois que o ASP.NET AJAX foi totalmente carregado. Portanto, adicione código para essa função para mostrar o controle ModalPopup, mas somente se `launchModal()` foi chamado antes de:

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

O `$find()` está procurando por um elemento nomeado na página de função e espera que a ID do servidor como um parâmetro. Portanto, `$find("mpe")` retorna a representação de cliente do controle ModalPopup; seu `show()` método permite que o pop-up aparecer.


[![O pop-up modal aparece quando qualquer um dos botões é clicado](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)

O pop-up modal aparece quando qualquer um dos botões é clicado ([clique para exibir a imagem em tamanho normal](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Avançar](using-modalpopup-with-a-repeater-control-cs.md)
