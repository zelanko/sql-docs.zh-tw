---
description: ODBC 資料指標程式庫錯誤碼
title: ODBC 資料指標程式庫錯誤碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 414de02eb7145006af4faa543735888082a3d6ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466133"
---
# <a name="odbc-cursor-library-error-codes"></a>ODBC 資料指標程式庫錯誤碼
> [!IMPORTANT]  
>  這項功能將會在未來版本的 Microsoft Data Access 元件中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用驅動程式和伺服器資料指標。  
  
 除了 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)中列出的 SQLSTATEs 之外，odbc 資料指標程式庫還會傳回下列。  
  
> [!NOTE]  
>  資料指標程式庫不會排序狀態記錄;驅動程式管理員和 ODBC 3。*x* 驅動程式負責排序狀態記錄。  
  
|SQLSTATE|描述|可以從傳回|  
|--------------|-----------------|--------------------------|  
|01000|資料指標不是可更新的。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|未使用資料指標程式庫。 載入失敗。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|未使用資料指標程式庫。 驅動程式支援不足。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|未使用資料指標程式庫。 版本與驅動程式管理員不符。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|驅動程式傳回 SQL_SUCCESS_WITH_INFO。 警告訊息已遺失。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|一般錯誤：無法建立檔案緩衝區。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般錯誤：無法從檔案緩衝區讀取。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般錯誤：無法寫入檔案緩衝區。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般錯誤：無法關閉或移除檔案緩衝區。|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|因為沒有系結的可搜尋資料行，所以無法執行定位要求。|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|因為結果集是由聯結條件所建立，所以無法執行定位的要求。|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|系結緩衝區超過區段大小上限。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|**SELECT**語句未產生結果集。|**SQLGetData**|  
|SL005|**SELECT** 語句包含 group by 子句。|**SQLGetData**|  
|SL006|定位要求不支援參數陣列。|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|順向 (nonbuffered) 資料指標上不允許**SQLGetData** 。|**SQLGetData**|  
|SL009|呼叫 **SQLFetch** 或 **SQLFetchScroll**之前未系結任何資料行。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** 在嘗試系結至內部緩衝區時傳回 SQL_ERROR。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|只有在呼叫 **SQLFetch** 或 **SQLFetchScroll**之後，語句選項才有效。|**SQLGetStmtAttr**|  
|SL012|當資料指標開啟時，語句系結可能不會變更。|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|已發出定位要求，但並非所有資料行計數位段都已緩衝處理。|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** 和 **SQLFetchScroll** 不能混用。|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
