---
title: 準備和執行命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f3de2bb729e2096e1b30aab12c402803036914b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911357"
---
# <a name="preparing-and-executing-commands"></a>準備和執行命令
命令會執行某些作業，針對基礎資料來源發行至提供者的指示。 SQL 陳述式，比方說，是 Microsoft SQL 資料提供者的命令。 在 ADO 中，命令通常會以所**命令**物件，雖然也可以透過發出簡單的命令**連線**或是**資料錄集**物件。  
  
 您可以使用**命令**要求從提供者，假設提供者可正確解譯命令字串的任何支援的作業類型的物件。 資料提供者的常見作業是查詢資料庫，並傳回在資料錄**資料錄集**，可以視為容器以保存結果和工具來檢視結果的物件。 如同許多 ADO 物件，有些**命令**物件集合、 方法或屬性，則可能會產生錯誤參考時，視提供者功能而定。  
  
 除了使用**命令**物件，您可以使用**Execute**方法**連接**物件或**開啟**方法**資料錄集**發出命令，並讓它執行的物件。 不過，您應該使用**命令**物件，如果您要重複使用您的程式碼中的命令，或如果您需要傳遞參數的詳細的資訊與您的命令。 本節稍後詳細說明這些案例。  
  
> [!NOTE]
>  某些**命令**s 可以傳回的結果集做為二進位資料流或單一**記錄**而**資料錄集**，如果這提供者支援。 此外，有些**命令**s 並非以傳回任何結果完全設定 （例如，SQL Update 查詢）。 本節將討論最常見的案例中，不過： 執行**命令**會傳回結果做為 s**資料錄集**物件。 如需有關傳回結果載入**記錄**s 或**Stream**s，請參閱[記錄和資料流](../../../ado/guide/data/records-and-streams.md)。  
  
 此章節包含下列主題。  
  
-   [Command 物件概觀](../../../ado/guide/data/command-object-overview.md)  
  
-   [建立和執行簡單的命令](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command 物件參數](../../../ado/guide/data/command-object-parameters.md)  
  
-   [使用命令呼叫預存程序](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [為連線物件上方法呼叫的預存程序](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [具名命令](../../../ado/guide/data/named-commands.md)  
  
-   [傳遞參數給具名命令](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
