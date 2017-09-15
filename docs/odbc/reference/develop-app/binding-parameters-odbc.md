---
title: "繫結參數 ODBC |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 20879f658c1fdc2ca8a4527f76a540ab2700b98f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="binding-parameters-odbc"></a>繫結參數 ODBC
SQL 陳述式中的每個參數必須有關聯，或*繫結，*給應用程式之前執行的陳述式中的變數。 當應用程式會將變數繫結至參數時，它描述該變數： 位址、 C 資料類型，等等，驅動程式。 它也會描述參數本身，SQL 資料類型、 有效位數，等等。 驅動程式會將此資訊儲存在結構中，它會維持為該陳述式，並使用的資訊來執行陳述式時，從變數擷取值。  
  
 參數可以繫結，或隨時之前執行的陳述式重新繫結。 如果執行陳述式之後，參數為不再重新繫結，繫結不適用直到再次執行陳述式。 若要將參數繫結至不同的變數，應用程式只會重新繫結與新的變數; 參數系統自動釋放之前的繫結。  
  
 直到不同的變數繫結至參數，直到所有參數藉由呼叫未繫都結變數會保留至參數繫結**SQLFreeStmt** SQL_RESET_PARAMS 選項時，或釋放陳述式之前。 基於這個理由，應用程式必須確定該變數未釋出直到之後未繫結。 如需詳細資訊，請參閱[Allocating 和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由於參數繫結只是儲存在陳述式的驅動程式所維護的結構中的資訊，您可以依照任何順序設定。 它們也是獨立執行的 SQL 陳述式。 例如，假設應用程式繫結三個參數，然後執行下列 SQL 陳述式：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 如果應用程式，然後立即執行的 SQL 陳述式  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 在相同的陳述式控制代碼，參數繫結上**插入**陳述式可用，因為這些是儲存在陳述式結構中的繫結。 在大部分情況下，這是不佳的程式設計作法，而且應該避免。 相反地，應用程式應該呼叫**SQLFreeStmt**解除繫結所有舊的參數，並接著將新的繫結的 SQL_RESET_PARAMS 選項。  
  
 此章節包含下列主題。  
  
-   [繫結參數標記](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [繫結參數 （具名參數） 的名稱](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [參數繫結位移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [描述參數](../../../odbc/reference/develop-app/describing-parameters.md)
