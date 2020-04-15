---
title: 依名稱結合參數(命名參數) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1e214f50488c4600ed39f76e91618cc5ce53de4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306369"
---
# <a name="binding-parameters-by-name-named-parameters"></a>依名稱繫結參數 (具名參數)
某些 DBMS 允許應用程式按名稱而不是按過程調用中的位置指定存儲過程的參數。 此參數稱為*命名參數*。 ODBC 支援使用命名參數。 在 ODBC 中,命名參數僅用於對儲存過程的調用,不能在其他 SQL 語句中使用。  
  
 驅動程式檢查 IPD SQL_DESC_UNNAMED欄位的值,以確定是否使用了命名參數。 如果未將SQL_DESC_UNNAMED設定為SQL_UNNAMED,則驅動程式將使用 IPD SQL_DESC_NAME 欄位中的名稱來標識參數。 要綁定參數,應用程式可以調用**SQLBindparameter**來指定參數資訊,然後可以調用**SQLSetDescField**來設置 IPD 的SQL_DESC_NAME欄位。 使用命名參數時,過程調用中的參數順序並不重要,並且忽略該參數的記錄編號。  
  
 未命名參數和命名參數之間的差異在於描述符的記錄編號與過程中參數編號之間的關係。 使用未命名參數時,第一個參數標記與參數描述符中的第一個記錄相關,而該記錄又與過程呼叫中的第一個參數(按創建順序)相關。 使用命名參數時,第一個參數標記仍與參數描述符的第一個記錄相關,但過程中的記錄編號與參數編號之間的關係不再存在。 命名參數不使用描述符記錄編號映射到過程參數位置;相反,描述符記錄名稱映射到過程參數名稱。  
  
> [!NOTE]  
>  如果啟用了 IPD 的自動填充,驅動程式將填充描述符,以便描述符記錄的順序將與過程定義中參數的順序匹配,即使使用了命名參數也是如此。  
  
 如果使用命名參數,則必須命名所有參數。 如果任何參數不是命名參數,則沒有命名參數。 如果存在命名參數和未命名參數的混合,則行為將依賴於驅動程式。  
  
 作為命名參數的範例,假設 SQL Server 儲存過程的定義如下:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 在此過程中,第一個參數@title_id, 的預設值為 1。 應用程式可以使用以下代碼調用此過程,以便它只指定一個動態參數。 此參數是名稱為「報價」\@的命名參數。  
  
```  
// Prepare the procedure invocation statement.  
SQLPrepare(hstmt, "{call test(?)}", SQL_NTS);  
  
// Populate record 1 of ipd.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                  30, 0, szQuote, 0, &cbValue);  
  
// Get ipd handle and set the SQL_DESC_NAMED and SQL_DESC_UNNAMED fields  
// for record #1.  
SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
// Assuming that szQuote has been appropriately initialized,  
// execute.  
SQLExecute(hstmt);  
```
