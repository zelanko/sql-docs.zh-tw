---
description: 建構搜尋的陳述式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b5ae620c4ba0292ff1133d70423cb85c360b1e53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339354"
---
# <a name="constructing-searched-statements"></a>建構搜尋的陳述式
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 為了支援定位的 update 和 delete 語句，資料指標程式庫會從定位語句中，建立搜尋的 **update** 或 **delete** 語句。 為了支援在資料區塊中呼叫 **SQLGetData** ，資料指標程式庫會建立搜尋的 **SELECT** 語句，以建立包含目前資料列的結果集。 在上述每個語句中， **WHERE** 子句會列舉儲存在快取中的每個系結資料行的值，此資料行會針對 **SQLColAttribute**中的 SQL_DESC_SEARCHABLE 欄位識別碼傳回 SQL_PRED_SEARCHABLE 或 SQL_PRED_BASIC。  
  
> [!CAUTION]  
>  資料指標程式庫所建立用來識別目前資料列的 **WHERE** 子句，可能無法識別任何資料列、識別不同的資料列，或識別一個以上的資料列。  
  
 如果定位的 update 或 delete 語句影響一個以上的資料列，資料指標程式庫只會針對資料指標所在的資料列更新資料列狀態陣列，並傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 (資料指標作業衝突) 。 如果語句未識別任何資料列，則資料指標程式庫不會更新資料列狀態陣列，並傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 (資料指標作業衝突) 。 應用程式可以呼叫 **SQLRowCount** 來判斷已更新或刪除的資料列數目。  
  
 如果用來將資料指標定位至**SQLGetData**的**SELECT**子句會識別一個以上的資料列，則不保證**SQLGetData**會傳回正確的資料。 如果未識別任何資料列， **SQLGetData** 會傳回 SQL_NO_DATA。  
  
 如果應用程式符合下列指導方針，則資料指標程式庫所建立的 **WHERE** 子句應該唯一識別目前的資料列，但不可能發生這種情況，例如當資料來源包含重複的資料列時。  
  
-   **系結可唯一識別資料列的資料行。** 如果系結資料行沒有唯一識別資料列，則由資料指標程式庫所建立的 **WHERE** 子句可能會識別一個以上的資料列。 在定位的 update 或 delete 語句中，這類子句可能會導致更新或刪除一個以上的資料列。 在 **SQLGetData**的呼叫中，這類子句可能會導致驅動程式傳回錯誤資料列的資料。 系結唯一索引鍵中的所有資料行，可確保每個資料列都能唯一識別。  
  
-   **配置夠大的資料緩衝區，而不會發生截斷。** 資料指標程式庫的快取是使用 **SQLBindCol**系結至結果集之資料列集緩衝區中值的複本。 如果資料置於這些緩衝區時遭到截斷，則在快取中也會被截斷。 從截斷的值所構成的 **WHERE** 子句可能無法正確地識別資料來源中的基礎資料列。  
  
-   **針對二進位 C 資料指定非 null 長度的緩衝區。** 只有當**SQLBindCol**中的*StrLen_or_IndPtr*引數為非 null 時，資料指標程式庫才會在其快取中配置長度緩衝區。 當 *TargetType* 引數 SQL_C_BINARY 時，資料指標程式庫需要二進位資料的長度，以從資料中建立 **WHERE** 子句。 如果 SQL_C_BINARY 資料行沒有長度緩衝區，而應用程式呼叫 **SQLGetData** 或嘗試執行定位的 update 或 delete 語句，則資料指標程式庫會傳回 SQL_ERROR 和 SQLSTATE SL014 (已發出定位要求，但並非所有資料行計數位段都已) 。  
  
-   **針對可為 null 的資料行指定非 null 長度的緩衝區。** 只有當**SQLBindCol**中的*StrLen_or_IndPtr*引數為非 null 時，資料指標程式庫才會在其快取中配置長度緩衝區。 由於 SQL_Null_DATA 儲存在長度緩衝區中，因此，資料指標程式庫會假設未指定長度緩衝區的任何資料行都不能為 null。 如果未針對可為 null 的資料行指定長度資料行，則資料指標程式庫會使用資料行的資料值來建立 **WHERE** 子句。 這個子句將無法正確識別資料列。
