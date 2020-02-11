---
title: 建立搜尋的語句 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8f24fe59da1377ea42900a8f1f0b89eb97125f3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019175"
---
# <a name="constructing-searched-statements"></a>建構搜尋的陳述式
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 為了支援定位的 update 和 delete 語句，資料指標程式庫會從定位語句中，建立搜尋的**update**或**delete**語句。 若要支援在資料區塊中呼叫**SQLGetData** ，資料指標程式庫會建立一個搜尋的**SELECT**語句，以建立包含目前資料列的結果集。 在上述每個語句中， **WHERE**子句會列舉在**SQLColAttribute**中針對 SQL_DESC_SEARCHABLE 欄位識別碼傳回 SQL_PRED_SEARCHABLE 或 SQL_PRED_BASIC 之每個系結資料行的快取中儲存的值。  
  
> [!CAUTION]  
>  用來識別目前資料列的資料指標程式庫所建立的**WHERE**子句，可能無法識別任何資料列、識別不同的資料列，或識別一個以上的資料列。  
  
 如果定位的 update 或 delete 語句會影響一個以上的資料列，則資料指標程式庫只會針對資料指標所在的資料列更新資料列狀態陣列，並傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 （資料指標作業衝突）。 如果語句未識別任何資料列，則資料指標程式庫不會更新資料列狀態陣列，並會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 （資料指標作業衝突）。 應用程式可以呼叫**SQLRowCount**來判斷已更新或刪除的資料列數目。  
  
 如果用來定位資料指標以呼叫**SQLGetData**的**SELECT**子句識別一個以上的資料列，則不保證**SQLGetData**會傳回正確的資料。 如果找不到任何資料列， **SQLGetData**就會傳回 SQL_NO_DATA。  
  
 如果應用程式符合下列方針，則資料指標程式庫所建立的**WHERE**子句應該唯一識別目前的資料列，但不可能發生這種情況，例如當資料來源包含重複的資料列時。  
  
-   **系結唯一識別資料列的資料行。** 如果系結的資料行不會唯一識別資料列，則資料指標程式庫所建立的**WHERE**子句可能會識別一個以上的資料列。 在定位的 update 或 delete 語句中，這類子句可能會導致更新或刪除一個以上的資料列。 在呼叫**SQLGetData**時，這類子句可能會導致驅動程式傳回錯誤資料列的資料。 將唯一索引鍵中的所有資料行系結，可確保每個資料列都有唯一的識別。  
  
-   **配置足以進行截斷的資料緩衝區。** 資料指標程式庫的快取是與**SQLBindCol**系結至結果集之資料列集緩衝區中的值複本。 如果資料放在這些緩衝區時遭到截斷，它也會在快取中被截斷。 從截斷的值所構成的**WHERE**子句可能無法正確識別資料來源中的基礎資料列。  
  
-   **針對二進位 C 資料指定非 null 長度的緩衝區。** 資料指標程式庫只有在**SQLBindCol**中的*StrLen_or_IndPtr*引數為非 null 時，才會在其快取中配置長度緩衝區。 當*TargetType*引數是 SQL_C_BINARY 時，資料指標程式庫會要求二進位資料的長度，以從資料中建立**WHERE**子句。 如果 SQL_C_BINARY 的資料行沒有長度緩衝區，而應用程式呼叫**SQLGetData**或嘗試執行定位的 update 或 delete 語句，則資料指標程式庫會傳回 SQL_ERROR 和 SQLSTATE SL014 （已發出定位要求，而不是所有資料行計數位段已緩衝處理）。  
  
-   **針對可為 null 的資料行指定非 null 長度的緩衝區。** 資料指標程式庫只有在**SQLBindCol**中的*StrLen_or_IndPtr*引數為非 null 時，才會在其快取中配置長度緩衝區。 因為 SQL_Null_DATA 儲存在長度緩衝區中，所以資料指標程式庫會假設沒有指定長度緩衝區的任何資料行都是不可為 null。 如果沒有為可為 null 的資料行指定長度資料行，則資料指標程式庫會建立一個**where**子句，該子句會使用資料行的資料值。 這個子句將無法正確識別資料列。
