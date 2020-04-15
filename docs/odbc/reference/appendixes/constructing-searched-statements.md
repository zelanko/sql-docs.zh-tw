---
title: 建構搜尋語句 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8b9a27aa9fc84aadc6659993de3e12e269631d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284738"
---
# <a name="constructing-searched-statements"></a>建構搜尋的陳述式
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 為了支援定位更新和刪除語句,游標庫從定位語句**構造搜索的更新**或**DELETE**語句。 為了支援對資料塊中的**SQLGetData**的調用,遊標庫構造一個搜尋的**SELECT**語句以創建包含當前數據行的結果集。 在每一個語句中 **,WHERE**子句都會枚舉存儲在緩存中為每個綁定列的值,這些值返回**SQLColAttribute**中SQL_DESC_SEARCHABLE字段標識符的SQL_PRED_SEARCHABLE或SQL_PRED_BASIC。  
  
> [!CAUTION]  
>  游標庫為標識當前行而構造的**WHERE**子句可能無法標識任何行、標識其他行或標識多行。  
  
 如果定位的更新或刪除語句影響多行,游標庫僅針對游標所定位的行更新行狀態陣列,並返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01001(Cursor 操作衝突)。 如果語句未標識任何行,則游標庫不會更新行狀態陣列,並返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01001(Cursor 操作衝突)。 應用程式可以調用**SQLRowCount**來確定更新或刪除的行數。  
  
 如果用於定位**SQLGetData**調用的游標的**SELECT**子句標識了多行,則**SQLGetData**不保證返回正確的數據。 如果**SQLGetData**未識別任何行,則返回SQL_NO_DATA。  
  
 如果應用程式符合以下準則,則游標庫構造的**WHERE**子句應唯一標識當前行,除非這是不可能的,例如數據源包含重複行時。  
  
-   **綁定唯一標識行的列。** 如果綁定列不唯一標識該行,則游標庫構造的**WHERE**子句可能會標識多行。 在定位的更新或刪除語句中,此類子句可能會導致更新或刪除多行。 在調用**SQLGetData**時,此類子句可能會導致驅動程式返回錯誤行的數據。 將所有列綁定到唯一的鍵中,可確保每行都唯一標識。  
  
-   **分配足夠大的數據緩衝區,以便不發生截斷。** 游標庫的緩存是使用**SQLBindCol**綁定到結果集的行集緩衝區中的值的副本。 如果數據被截斷,當它被放置在這些緩衝區中時,它也會被截斷在緩存中。 由截斷值構造的**WHERE**子句可能無法正確標識數據源中的基礎行。  
  
-   **為二進位C數據指定非空長度緩衝區。** 僅當**SQLBindCol**中的*StrLen_or_IndPtr*參數為非空時,游標庫才會在其緩存中分配長度緩衝區。 當*TargetType*參數SQL_C_BINARY時,遊標庫需要二進位數據的長度才能從數據構造**WHERE**子句。 如果SQL_C_BINARY列沒有長度緩衝區,並且應用程式調用**SQLGetData**或嘗試執行定位的更新或刪除語句,則游標庫將返回SQL_ERROR和 SQLSTATE SL014(已發出定位請求,並非所有列計數位段都已緩衝)。  
  
-   **為空列指定非空長度緩衝區。** 僅當**SQLBindCol**中的*StrLen_or_IndPtr*參數為非空時,游標庫才會在其緩存中分配長度緩衝區。 由於SQL_NULL_DATA存儲在長度緩衝區中,因此游標庫假定未為其指定長度緩衝區的任何列都是不可虛無的。 如果未為空列指定長度列,則游標庫將構造一個**WHERE**子句,該子句使用列的數據值。 此子句無法正確標識該行。
