---
title: ODBC 的目錄功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6731018b99f2f3043e48ee7c174a08cb9ef71fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306229"
---
# <a name="catalog-functions-in-odbc"></a>ODBC 中的目錄函式
ODBC 包含以下目錄函數:  
  
|函式|描述|  
|--------------|-----------------|  
|**SQLTables**|傳回資料來源中的目錄、架構、表或表類型的清單。|  
|**SQLColumns**|傳回一個或多個表中的列清單。|  
|**SQLStatistics**|返回有關單個表的統計資訊清單。 還會返回與該表關聯的索引清單。|  
|**SQLSpecialColumns**|返回唯一標識單個表中的行的列清單。 還會返回該表中自動更新的列的清單。|  
|**SQLPrimaryKeys**|返回組成單個表的主鍵的列清單。|  
|**SQLForeignKeys**|返回單個表中的外鍵清單或引用單個表的其他表中的外鍵清單。|  
|**SQLTablePrivileges**|返回與一個或多個表關聯的許可權清單。|  
|**SQLColumnPrivileges**|返回與單個表中的一個或多個列關聯的許可權清單。|  
|**SQLProcedures**|返回數據源中的過程清單。|  
|**SQLProcedureColumns**|返回單個過程的結果集中的輸入和輸出參數、返回值和列的清單。|  
|**SQLGetTypeInfo**|傳回資料來源支援的 SQL 資料類型的清單。 這些資料類型通常用於**創建表**和**ALTER TABLE**語句。|  
  
 由於**SQLTables、SQLColumns、SQL****統計**和**SQL 特別列**符合開放組 CLI,並且**SQLGetTypeInfo**符合 ISO 92 **SQLTables** CLI,因此大多數驅動程式都實現了它們。 其餘目錄函數處於ODBC一致性級別。  
  
 此章節包含下列主題。  
  
-   [目錄函式所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [目錄函式中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [結構描述檢視](../../../odbc/reference/develop-app/schema-views.md)
