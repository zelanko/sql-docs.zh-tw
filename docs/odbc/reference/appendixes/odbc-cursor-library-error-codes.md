---
title: ODBC 游標庫錯誤代碼 |微軟文件
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
ms.openlocfilehash: c263ce53c41546e63dc2a830d3db3b903e2e3515
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301429"
---
# <a name="odbc-cursor-library-error-codes"></a>ODBC 資料指標程式庫錯誤碼
> [!IMPORTANT]  
>  此功能將在Microsoft資料存取元件的未來版本中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 而是使用驅動程式和伺服器游標。  
  
 ODBC 遊標庫除了[在 ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)中列出的 SQLSTAT 外,還返回以下 SQLSTAT。  
  
> [!NOTE]  
>  游標庫不排序狀態記錄;因此,游標庫不對狀態記錄進行排序。驅動程式管理員和ODBC 3。*x*驅動程式負責訂購狀態記錄。  
  
|SQLSTATE|描述|可以從|  
|--------------|-----------------|--------------------------|  
|01000|游標不可上用。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|不使用游標庫。 載入失敗。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|不使用游標庫。 驅動程式支援不足。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|不使用游標庫。 版本與驅動程式管理員不匹配。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|驅動程式返回SQL_SUCCESS_WITH_INFO。 警告消息已丟失。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|一般錯誤:無法創建檔緩衝區。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般錯誤:無法從檔緩衝區讀取。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般錯誤:無法寫入檔緩衝區。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般錯誤:無法關閉或刪除檔緩衝區。|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|無法執行定位請求,因為未綁定任何可搜索列。|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|無法執行定位請求,因為結果集由聯接條件創建。|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|綁定緩衝區超過最大段大小。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|結果集不是由**SELECT**語句生成的。|**SQLGetData**|  
|SL005|**SELECT**語句包含一個 GROUP BY 子句。|**SQLGetData**|  
|SL006|定位請求不支援參數陣列。|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData**不允許在僅轉發(非緩衝)游標上。|**SQLGetData**|  
|SL009|在調用**SQLFetch**或**SQLFetchScroll**之前,沒有綁定任何列。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|在嘗試綁定到內部緩衝區期間 **,SQLBindCol**返回SQL_ERROR。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|語句選項僅在調用**SQLFetch**或**SQLFetchScroll**後才有效。|**SQLGetStmtAttr**|  
|SL012|打開遊標時,不能更改語句綁定。|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|已發出定位請求,並且並非所有列計數位段都進行了緩衝。|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch**和**SQLFetchScroll**不能混合。|**SQL 延伸**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
