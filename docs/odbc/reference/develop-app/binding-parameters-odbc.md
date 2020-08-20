---
description: 繫結參數 ODBC
title: Binding 參數 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9893d6611ad2bfc7107df1cd2d4ffe72dbf32fad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499951"
---
# <a name="binding-parameters-odbc"></a>繫結參數 ODBC
在執行語句之前，SQL 語句中的每個參數都必須 *關聯或系* 結至應用程式中的變數。 當應用程式將變數系結至參數時，它會對驅動程式描述該變數位址、C 資料類型等等。 它也會描述參數本身-SQL 資料類型、精確度等等。 驅動程式會將這項資訊儲存在它針對該語句所維護的結構中，並在執行語句時，使用此資訊來抓取變數中的值。  
  
 在執行語句之前，您隨時都可以系結或重新系結參數。 如果在執行語句之後重新系結參數，則在執行語句之前，不會套用系結。 為了將參數系結至不同的變數，應用程式只會將參數與新變數重新系結;系統會自動釋放先前的系結。  
  
 除非將不同的變數系結至參數，否則變數會保持系結至參數，直到所有參數都透過 SQL_RESET_PARAMS 選項來呼叫 **SQLFreeStmt** ，或直到釋放語句為止。 基於這個理由，應用程式必須確定變數在解除系結之後才會被釋放。 如需詳細資訊，請參閱配置 [和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 因為參數系結只是儲存在語句的驅動程式中的資訊，因此可以依任何順序進行設定。 它們也與執行的 SQL 語句無關。 例如，假設應用程式系結三個參數，然後執行下列 SQL 語句：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 如果應用程式接著立即執行 SQL 語句  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 在相同的語句控制碼上，會使用 **INSERT** 語句的參數系結，因為它們是儲存在語句結構中的系結。 在大部分的情況下，這是不佳的程式設計實務，應予以避免。 相反地，應用程式應該使用 SQL_RESET_PARAMS 選項來呼叫 **SQLFreeStmt** ，以解除所有舊參數的系結，然後系結新的參數。  
  
 此章節包含下列主題。  
  
-   [繫結參數標記](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [依名稱繫結參數 (具名參數)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [參數繫結位移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [描述參數](../../../odbc/reference/develop-app/describing-parameters.md)
