---
title: 系結參數 ODBC |Microsoft Docs
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
ms.openlocfilehash: 6e314bb9e3a1a979976a450e2a45a286ec54dfe7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306379"
---
# <a name="binding-parameters-odbc"></a>繫結參數 ODBC
在執行語句之前，SQL 語句中的每個參數都必須與應用程式中的變數相關*聯或系*結。 當應用程式將變數系結至參數時，它會描述該驅動程式的變數位址、C 資料類型等等。 它也會描述參數本身-SQL 資料類型、有效位數等等。 驅動程式會將這項資訊儲存在它為該語句維護的結構中，並在執行語句時，使用此資訊來抓取變數中的值。  
  
 在執行語句之前，可以隨時系結或重新系結參數。 如果參數在執行語句之後重新系結，則在再次執行語句之前，不會套用系結。 若要將參數系結至不同的變數，應用程式只會將參數重新系結至新的變數。會自動釋放先前的系結。  
  
 變數會維持系結至參數，直到不同的變數系結至參數為止，直到所有參數都已解除系結，方法是使用 SQL_RESET_PARAMS 選項呼叫**SQLFreeStmt** ，或在釋放語句之前。 基於這個理由，應用程式必須確定變數不會釋放，直到它們解除系結為止。 如需詳細資訊，請參閱配置[和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 因為參數系結只是儲存在語句的驅動程式所維護的結構中的資訊，所以可以依任何順序進行設定。 它們也與執行的 SQL 語句無關。 例如，假設應用程式會系結三個參數，然後執行下列 SQL 語句：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 如果應用程式接著立即執行 SQL 語句  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 在相同的語句控制碼上，會使用**INSERT**語句的參數系結，因為這些系結是儲存在語句結構中的系結。 在大部分情況下，這是不佳的程式設計實務，應予以避免。 相反地，應用程式應該使用 SQL_RESET_PARAMS 選項來呼叫**SQLFreeStmt** ，以解除系結所有舊的參數，然後再系結新的參數。  
  
 此章節包含下列主題。  
  
-   [繫結參數標記](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [依名稱繫結參數 (具名參數)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [參數繫結位移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [描述參數](../../../odbc/reference/develop-app/describing-parameters.md)
