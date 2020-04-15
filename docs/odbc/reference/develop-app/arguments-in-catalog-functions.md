---
title: 目錄函數中的參數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 819c10d0b137d5e0999c1e10bf22810392509f76
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288164"
---
# <a name="arguments-in-catalog-functions"></a>目錄函式中的引數
所有目錄函數都接受應用程式可以限制返回的數據範圍的參數。 例如,以下代碼中對**SQLTable**的第一次和第二次調用傳回一個包含所有表資訊的結果集,而第三個呼叫傳回有關 Orders 表的資訊:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 目錄函數字串參數分為四種不同類型:普通參數 (OA)、模式值參數 (PV)、標識符參數 (ID) 和值清單參數 (VL)。 大多數字串參數可以是兩種不同類型的類型之一,具體取決於SQL_ATTR_METADATA_ID語句屬性的值。 下表列出了每個目錄函數的參數,並描述了SQL_TRUE或SQL_ATTR_METADATA_ID值的SQL_FALSE參數的類型。  
  
|函式|引數|SQL_時鍵入<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|SQL_時鍵入<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*目錄名稱**架構名稱**表格**名稱 欄位名稱*|OA OA OA 光伏|ID ID ID ID|  
|**SQLColumns**|*目錄名稱**架構名稱**表格**名稱 欄位名稱*|OA 光伏光伏光伏|ID ID ID ID|  
|**SQLForeignKeys**|*PK 目錄名稱**PK 名稱* *PKtable 名稱* *FKcatalog 名稱* *FKschema 名稱* *FKtable 名稱*|OA OA OA OA OA OA|ID ID ID ID ID ID|  
|**SQLPrimaryKeys**|*目錄名稱**架構名稱**表格名稱*|OA OA OA|ID ID ID|  
|**SQLProcedureColumns**|*目錄名稱**架構名稱* *Procname* *欄位名稱*|OA 光伏光伏光伏|ID ID ID ID|  
|**SQLProcedures**|*目錄名稱**架構名稱* *ProcName*|OA 光伏光伏|ID ID ID|  
|**SQLSpecialColumns**|*目錄名稱**架構名稱**表格名稱*|OA OA OA|ID ID ID|  
|**SQLStatistics**|*目錄名稱**架構名稱**表格名稱*|OA OA OA|ID ID ID|  
|**SQLTablePrivileges**|*目錄名稱**架構名稱**表格名稱*|OA 光伏光伏|ID ID ID|  
|**SQLTables**|*目錄名稱**架構名稱**表格表型**態*|光伏光伏光伏 VL|ID ID ID VL|  
  
 此章節包含下列主題。  
  
-   [一般引數](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [識別碼引數](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [值清單引數](../../../odbc/reference/develop-app/value-list-arguments.md)
