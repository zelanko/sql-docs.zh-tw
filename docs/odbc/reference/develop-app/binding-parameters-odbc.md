---
title: 繫結參數 ODBC |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306379"
---
# <a name="binding-parameters-odbc"></a>繫結參數 ODBC
在執行語句之前,SQL 語句中的每個參數都必須關聯或*綁定*到應用程式中的變數。 當應用程式將變數綁定到參數時,它將該變數 (位址、 C 資料類型等 ) 描述到驅動程式。 它還描述了參數本身 - SQL 數據類型、精度等。 驅動程式將此資訊存儲在它為該語句維護的結構中,並使用該資訊在執行語句時從變數中檢索值。  
  
 在執行語句之前,可以隨時綁定或反彈參數。 如果參數在執行語句后反彈,則綁定在語句再次執行之前不適用。 要將參數綁定到其他變數,應用程式只需將參數與新變數重新綁定即可;以前的綁定將自動釋放。  
  
 變數將保留到參數,直到將不同的變數綁定到參數,直到所有參數通過使用 SQL_RESET_PARAMS 選項調用**SQLFreeStmt**或直到語句發布來取消綁定。 因此,應用程式必須確保在變數未綁定之前不會釋放它們。 有關詳細資訊,請參閱[分配和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由於參數綁定只是存儲在語句的驅動程式維護的結構中的資訊,因此可以按任何順序設置它們。 它們也獨立於執行的 SQL 語句。 例如,假設應用程式綁定三個參數,然後執行以下 SQL 語句:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 如果應用程式然後立即執行 SQL 語句  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 在同一語句句柄上,使用**INSERT**語句的參數綁定,因為這些綁定存儲在語句結構中。 在大多數情況下,這是一種糟糕的程式設計實踐,應避免使用。 相反,應用程式應使用SQL_RESET_PARAMS選項調用**SQLFreeStmt,** 以取消綁定所有舊參數,然後綁定新參數。  
  
 此章節包含下列主題。  
  
-   [繫結參數標記](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [依名稱繫結參數 (具名參數)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [參數繫結位移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [描述參數](../../../odbc/reference/develop-app/describing-parameters.md)
