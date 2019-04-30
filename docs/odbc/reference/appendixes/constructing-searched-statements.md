---
title: 建構搜尋的陳述式 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 616e4241c6d28e846a56116a70e79254e13dd5fb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224561"
---
# <a name="constructing-searched-statements"></a>建構搜尋的陳述式
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 若要支援定位的 update 和 delete 陳述式，資料指標程式庫建構搜尋**更新**或是**刪除**從定位陳述式的陳述式。 若要支援呼叫**SQLGetData**區塊中的資料，資料指標程式庫建構搜尋**選取**陳述式來建立結果集，其中包含目前資料列。 在每個陳述式，**何處**子句列舉傳回 SQL_PRED_SEARCHABLE 或 SQL_PRED_BASIC SQL_DESC_SEARCHABLE 欄位識別項中的每個繫結資料行的快取中儲存的值**SQLColAttribute**。  
  
> [!CAUTION]  
>  **其中**建構的資料指標程式庫，以識別目前的資料列的子句無法識別的任何資料列、 找出不同的資料列，或識別一個以上的資料列。  
  
 如果定位的 update 或 delete 陳述式會影響多個資料列，資料指標程式庫會更新資料列狀態陣列，只會針對資料列的資料指標的位置，傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 （資料指標作業衝突）。 如果陳述式不會識別任何資料列，資料指標程式庫不會更新資料列狀態陣列，並傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 （資料指標作業衝突）。 應用程式可以呼叫**SQLRowCount**來判斷已更新或刪除資料列數目。  
  
 如果**選取 **子句用來定位資料指標來呼叫**SQLGetData**識別一個以上的資料列**SQLGetData**不保證會傳回正確的資料。 如果它不會識別任何資料列， **SQLGetData**傳回 sql_no_data 為止。  
  
 如果應用程式符合下列指導方針中，**其中**資料指標程式庫所建構的子句應專門用於識別目前的資料列，除非這是不可能的例如當資料來源包含重複資料列。  
  
-   **唯一識別資料列的資料行繫結。** 如果繫結的資料行無法唯一識別資料列，**其中**資料指標程式庫所建構的子句可能會識別多個資料列。 在定位的 update 或 delete 陳述式中，這類子句可能會導致多個要更新或刪除資料列。 在呼叫**SQLGetData**，這類子句可能會導致驅動程式傳回錯誤的資料列的資料。 唯一索引鍵中的所有資料行繫結，可保證唯一識別每個資料列。  
  
-   **配置資料緩衝區夠大的不截斷，就會發生。** 資料指標程式庫的快取是繫結至結果集的資料列集緩衝區中的值的複本**SQLBindCol**。 如果資料遭到截斷，它會放置在這些緩衝區時，它也會截斷快取中。 A**其中**子句建構從截斷的值可能無法正確識別基礎資料來源中的資料列。  
  
-   **指定非 null 長度為 C 的二進位資料的緩衝區。** 資料指標程式庫配置長度的緩衝區，在其快取才*StrLen_or_IndPtr*中的引數**SQLBindCol**為非 null。 當*TargetType*引數為 SQL_C_BINARY，資料指標程式庫需要建構的二進位資料的長度**其中**子句的資料。 如果沒有任何長度的緩衝區 SQL_C_BINARY 資料行和應用程式會呼叫**SQLGetData**或嘗試執行定位的 update 或 delete 陳述式，此資料指標程式庫會傳回 SQL_ERROR，而且 SQLSTATE SL014 （定位發出要求，並非所有的資料行計數欄位已緩衝處理。）  
  
-   **指定非 null 長度的緩衝區，可為 null 的資料行。** 資料指標程式庫配置長度的緩衝區，在其快取才*StrLen_or_IndPtr*中的引數**SQLBindCol**為非 null。 因為 SQL_NULL_DATA 儲存在長度的緩衝區，資料指標程式庫會假設任何長度的緩衝區已指定任何資料行是不可為 null。 如果為 null 的資料行不指定任何長度的資料行，資料指標程式庫會建構**其中**會使用資料行的資料值的子句。 這個子句不會正確地識別資料列。
