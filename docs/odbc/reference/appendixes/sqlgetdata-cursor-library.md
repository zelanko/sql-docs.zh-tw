---
title: SQLGetData （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e3009b4e3bed6fc871ecfd1aab4e2af2f1f1c86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188764"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLGetData**資料指標程式庫中的函式。 如需一般資訊**SQLGetData**，請參閱[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
 資料指標程式庫會實作**SQLGetData**首先透過建構**選取**陳述式搭配**其中**列舉每個繫結其快取中儲存之值的子句目前的資料列中的資料行。 接著它會執行**選取** 陳述式以重新選取資料列，然後呼叫**SQLGetData**中驅動程式 （而不是快取） 資料來源擷取資料。  
  
> [!CAUTION]  
>  **其中**建構的資料指標程式庫，以識別目前的資料列的子句無法識別的任何資料列、 找出不同的資料列，或識別一個以上的資料列。 如需詳細資訊，請參閱 <<c0> [ 建構搜尋的陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 如果 SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE， **SQLGetData**可呼叫資料行 0 傳回書籤的資料。  
  
 若要呼叫**SQLGetData**受到下列限制：  
  
-   **SQLGetData**無法為順向資料指標呼叫。  
  
-   **SQLGetData**只有在符合下列條件時，才可以呼叫：**選取**產生的結果集的陳述式;**選取**陳述式未包含聯結， **UNION**子句，或有**GROUP BY**子句，並使用別名或運算式選取清單中的任何資料行已不會與繫結**SQLBindCol**。  
  
-   如果此驅動程式支援只有一個作用中陳述式，資料指標程式庫，將會擷取結果集之前執行的 rest**選取** 陳述式，並呼叫**SQLGetData**。
