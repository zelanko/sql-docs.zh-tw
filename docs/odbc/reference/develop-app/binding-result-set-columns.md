---
title: 繫結結果集列 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 558ceb79d42d82477b70a028395de82cc023c170
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306359"
---
# <a name="binding-result-set-columns"></a>繫結結果集資料行
應用程式可以綁定結果集的任意數量或數量少的列,包括綁定無列。 獲取一行數據時,驅動程式將綁定列的數據返回給應用程式。 應用程式是否綁定結果集中的所有列取決於應用程式。 例如,生成報表的應用程式通常具有固定格式;此類應用程式創建一個結果集,其中包含報表中使用的所有列,然後綁定和檢索所有這些列的數據。 顯示充滿數據的螢幕的應用程序有時允許使用者決定要顯示哪些列;此類應用程式創建一個結果集,其中包含使用者可能需要的所有列,但僅為用戶選擇的列綁定和檢索數據。  
  
 可以通過調用**SQLGetData**從未綁定列檢索數據。 這通常稱為檢索長數據,這些數據通常超過單個緩衝區的長度,並且必須在零件中檢索。  
  
 列可以隨時綁定,即使在已提取行之後也是如此。 但是,新綁定直到下次提取行才會生效;它們不應用於已提取的行中的數據。  
  
 變數將保留到列,直到將另一個變數綁定到列,直到該列通過調用**SQLBindCol**與空指標作為變數的位址來取消綁定,直到所有列通過使用 SQL_UNBIND 選項調用**SQLFreeStmt**或直到語句發佈而取消綁定。 因此,應用程式必須確保所有綁定變數都保持有效,只要它們被綁定。 有關詳細資訊,請參閱[分配和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由於列綁定只是與語句結構關聯的資訊,因此可以按任何順序設置它們。 它們也獨立於結果集。 例如,假設應用程式綁定由以下 SQL 語句生成的結果集的列:  
  
```  
SELECT * FROM Orders  
```  
  
 如果應用程式後執行 SQL 語句  
  
```  
SELECT * FROM Lines  
```  
  
 在同一語句句柄上,第一個結果集的列綁定仍然有效,因為這些綁定是存儲在語句結構中的綁定。 在大多數情況下,這是一種糟糕的程式設計實踐,應避免使用。 相反,應用程式應使用SQL_UNBIND選項調用**SQLFreeStmt,** 以取消綁定所有舊列,然後綁定新列。
