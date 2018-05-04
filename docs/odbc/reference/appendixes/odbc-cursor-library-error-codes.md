---
title: ODBC 資料指標程式庫錯誤碼 |Microsoft 文件
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
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2c510ff777c2715955e594f7883daf5ee83b693
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-cursor-library-error-codes"></a>ODBC 資料指標程式庫的錯誤碼
> [!IMPORTANT]  
>  這項功能會在 Microsoft 資料存取元件的未來版本中移除。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用驅動程式和伺服器資料指標。  
  
 ODBC 資料指標程式庫傳回除了所列的下列 Sqlstate [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)。  
  
> [!NOTE]  
>  資料指標程式庫不會排序狀態記錄。驅動程式管理員和 ODBC 3。*x*驅動程式必須負責排序狀態記錄。  
  
|SQLSTATE|Description|可從傳回|  
|--------------|-----------------|--------------------------|  
|01000|資料指標不是可更新。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|不使用資料指標程式庫。 載入失敗。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|不使用資料指標程式庫。 不足的驅動程式支援。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|不使用資料指標程式庫。 版本不相符的驅動程式管理員。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|驅動程式會傳回 SQL_SUCCESS_WITH_INFO。 警告訊息已遺失。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|就會傳回 S1000|一般的錯誤： 無法建立檔案緩衝區。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|就會傳回 S1000|一般的錯誤： 無法從緩衝區讀取。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|就會傳回 S1000|一般的錯誤： 無法寫入檔案緩衝區。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|就會傳回 S1000|一般的錯誤： 無法關閉或移除檔案緩衝區。|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|無法執行定位的要求，因為沒有可搜尋的資料行已繫結。|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|無法執行定位的要求，因為聯結條件建立結果集。|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|繫結的緩衝區超過最大區段大小。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|結果集不由產生**選取**陳述式。|**SQLGetData**|  
|SL005|**選取**陳述式包含 GROUP BY 子句。|**SQLGetData**|  
|SL006|參數陣列不支援定位要求。|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData**順向的 （非緩衝） 資料指標上不允許。|**SQLGetData**|  
|SL009|沒有資料行已繫結之前呼叫**SQLFetch**或**SQLFetchScroll**。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol**期間嘗試繫結至內部緩衝區傳回 SQL_ERROR。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|陳述式選項只有在呼叫之後才有效**SQLFetch**或**SQLFetchScroll**。|**SQLGetStmtAttr**|  
|SL012|資料指標開啟時，可能不會變更陳述式繫結。|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|發出定位的要求，並非所有的資料行計數欄位已緩衝處理。|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch**和**SQLFetchScroll**不能混合。|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
