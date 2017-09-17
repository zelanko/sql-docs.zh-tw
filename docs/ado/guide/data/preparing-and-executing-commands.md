---
title: "準備和執行命令 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f566d3fb0c639e5f7cb7214d8cf467312ae7f28d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="preparing-and-executing-commands"></a>準備和執行命令
命令會指示發行給提供者執行某些作業，對基礎資料來源。 SQL 陳述式，比方說，是 Microsoft SQL 資料提供者的命令。 在 ADO 中，命令通常由**命令**物件，不過也可以透過發出簡單命令**連接**或**資料錄集**物件。  
  
 您可以使用**命令**要求作業的任何支援的類型，從提供者，並假設提供者可正確解譯命令字串的物件。 資料提供者的常見作業就是查詢資料庫並傳回記錄中的**資料錄集**物件，可以視為容器，以保留結果且以檢視結果的工具。 如同許多 ADO 物件一樣，有些**命令**物件集合、 方法或屬性可能會產生錯誤參考時，根據提供者的功能。  
  
 除了使用**命令**物件，您可以使用**Execute**方法**連接**物件或**開啟**方法**資料錄集**發出命令，並讓它執行的物件。 不過，您應該使用**命令**物件，如果您需要重複使用您的程式碼中的命令，或如果您需要傳遞參數的詳細的資訊與您的命令。 在本節稍後詳細涵蓋這些案例。  
  
> [!NOTE]
>  某些**命令**s 可以傳回的結果集為二進位資料流或單一**記錄**而**資料錄集**，如果這提供者支援。 此外，某些**命令**s 不是傳回任何結果集隨時 （例如，SQL 更新查詢）。 本節將討論最常見的案例，不過： 執行**命令**，它會傳回結果做為**資料錄集**物件。 如需有關傳回結果至**記錄**s 或**資料流**s，請參閱[記錄和資料流](../../../ado/guide/data/records-and-streams.md)。  
  
 此章節包含下列主題。  
  
-   [命令物件概觀](../../../ado/guide/data/command-object-overview.md)  
  
-   [建立和執行簡單的命令](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [命令物件參數](../../../ado/guide/data/command-object-parameters.md)  
  
-   [呼叫預存程序使用的命令](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [為連線物件上的方法呼叫的預存程序](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [具名的命令](../../../ado/guide/data/named-commands.md)  
  
-   [將參數傳遞至具名的命令](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
