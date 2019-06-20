---
title: 繫結參數 ODBC |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d62c0864678e116e30a0673bdf2625d70de0cedd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199603"
---
# <a name="binding-parameters-odbc"></a>繫結參數 ODBC
SQL 陳述式中的每個參數必須是相關聯，或*繫結，* 給應用程式之前執行的陳述式中的變數。 當應用程式會將變數繫結至參數時，它會描述該變數-位址、 C 資料類型等位，驅動程式。 它也會描述參數本身-SQL 資料類型、 有效位數和等等。 驅動程式會將此資訊儲存在結構中，它會維護該陳述式，並從變數擷取值，陳述式執行時使用的資訊。  
  
 參數可以繫結，或在任何時間執行的陳述式之前重新繫結。 如果在執行陳述式之後，會重新繫結參數，直到再次執行陳述式，不會套用繫結。 若要將參數繫結至不同的變數，應用程式只會重新繫結與新的變數; 參數先前的繫結就會自動釋放。  
  
 變數在不同的變數繫結至參數，直到所有的參數會藉由呼叫未繫結直到繫結至參數**SQLFreeStmt** SQL_RESET_PARAMS 選項，或直到釋放陳述式。 基於這個理由，必須確定，變數不會釋放之前未繫結之後，這些應用程式。 如需詳細資訊，請參閱 < [Allocating 及釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 參數繫結都只是儲存在結構中由陳述式的驅動程式所維護的資訊，因為它們可以依任何順序設定。 它們也是獨立執行的 SQL 陳述式。 例如，假設應用程式繫結三個參數，並接著執行下列 SQL 陳述式：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 如果應用程式會接著立即執行的 SQL 陳述式  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 在相同的陳述式控制代碼的參數繫結上**插入**陳述式會使用，因為這些是儲存在陳述式結構中的繫結。 在大部分情況下，這是不良的程式設計做法，而且應該予以避免。 相反地，應用程式應該呼叫**SQLFreeStmt**解除繫結所有舊的參數，然後將新的繫結的 SQL_RESET_PARAMS 選項。  
  
 此章節包含下列主題。  
  
-   [繫結參數標記](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [依名稱繫結參數 (具名參數)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [參數繫結位移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [描述參數](../../../odbc/reference/develop-app/describing-parameters.md)
