---
title: 建構搜尋陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fa7d3b27e483ea628dcdf0c9d44766b3142cb94
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="constructing-searched-statements"></a>建構搜尋陳述式
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 若要支援定位的 update 和 delete 陳述式，資料指標程式庫建構搜尋**更新**或**刪除**定位陳述式中的陳述式。 若要支援呼叫**SQLGetData**區塊中的資料，資料指標程式庫建構搜尋**選取**陳述式來建立結果集，其中包含目前資料列。 在每個陳述式，**其中**子句列舉傳回 SQL_PRED_SEARCHABLE 或 SQL_PRED_BASIC SQL_DESC_SEARCHABLE 欄位識別項中每個繫結資料行的快取中儲存的值**SQLColAttribute**。  
  
> [!CAUTION]  
>  **其中**子句所識別的目前資料列的資料指標程式庫建構無法識別任何資料列、 識別不同的資料列，或識別一個以上的資料列。  
  
 定位的更新或刪除陳述式會影響多個資料列，如果資料指標程式庫會更新資料列狀態陣列，僅針對資料列的資料指標的位置，傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 （資料指標作業衝突）。 如果陳述式不會識別任何資料列，資料指標程式庫不會更新資料列狀態陣列，並傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01001 （資料指標作業衝突）。 應用程式可以呼叫**SQLRowCount**來判斷已更新或刪除資料列數目。  
  
 如果**選取**子句用來定位資料指標進行呼叫**SQLGetData**識別一個以上的資料列， **SQLGetData**不保證會傳回正確的資料。 如果並未識別任何資料列， **SQLGetData**傳回 sql_no_data 為止。  
  
 如果應用程式符合下列指導方針，**其中**資料指標程式庫所建構的子句應專門用於識別目前的資料列，除非這是不可能，例如當資料來源包含重複項目資料列。  
  
-   **唯一識別資料列的資料行繫結。** 如果繫結的資料行沒有唯一識別資料列，**其中**子句資料指標程式庫所建構，可能會識別多個資料列。 定位的更新或刪除陳述式中，在這類子句可能會導致多個要更新或刪除資料列。 在呼叫**SQLGetData**，這類子句可能會導致驅動程式傳回錯誤的資料列的資料。 唯一索引鍵中的繫結的所有資料行可保證唯一識別每個資料列。  
  
-   **配置資料緩衝區夠大的不截斷。** 資料指標程式庫的快取是一份繫結至結果集的資料列集緩衝區中的值**SQLBindCol**。 如果資料遭到截斷時，它會放在這些緩衝區中，它也被截斷快取中。 A**其中**子句建構從截斷的值可能無法正確識別基礎資料來源中的資料列。  
  
-   **指定非 null 長度 C 的二進位資料的緩衝區。** 資料指標程式庫配置長度的緩衝區，其快取才會在中*StrLen_or_IndPtr*引數中的**SQLBindCol**為非 null。 當*TargetType*引數為 SQL_C_BINARY，資料指標程式庫需要長度的二進位資料來建構**其中**子句的資料。 如果沒有任何長度的緩衝區 SQL_C_BINARY 資料行和應用程式會呼叫**SQLGetData**或嘗試執行定位的更新或刪除陳述式中，資料指標程式庫傳回 SQL_ERROR 並 SQLSTATE SL014 （定位發出要求，並非所有的資料行計數欄位已緩衝處理。）  
  
-   **指定非 null 長度的緩衝區，可為 null 的資料行。** 資料指標程式庫配置長度的緩衝區，其快取才會在中*StrLen_or_IndPtr*引數中的**SQLBindCol**為非 null。 長度的緩衝區中儲存 SQL_NULL_DATA，因為資料指標程式庫假設任何長度的緩衝區會指定任何資料行不可為 null。 如果為 null 的資料行指定長度的資料行，資料指標程式庫建構**其中**會使用資料行的資料值的子句。 這個子句不會正確地識別資料列。
