---
title: ODBC 中的目錄函數 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306229"
---
# <a name="catalog-functions-in-odbc"></a>ODBC 中的目錄函式
ODBC 包含下列目錄函數：  
  
|函式|描述|  
|--------------|-----------------|  
|**SQLTables**|傳回資料來源中的目錄、架構、資料表或資料表類型的清單。|  
|**SQLColumns**|傳回一或多個資料表中的資料行清單。|  
|**SQLStatistics**|傳回單一資料表的統計資料清單。 也會傳回與該資料表相關聯的索引清單。|  
|**SQLSpecialColumns**|傳回可唯一識別單一資料表中之資料列的資料行清單。 也會傳回該資料表中自動更新的資料行清單。|  
|**SQLPrimaryKeys**|傳回組成單一資料表之主鍵的資料行清單。|  
|**SQLForeignKeys**|傳回單一資料表中的外鍵清單，或參考單一資料表之其他資料表中的外鍵清單。|  
|**SQLTablePrivileges**|傳回與一或多個資料表相關聯的許可權清單。|  
|**SQLColumnPrivileges**|傳回與單一資料表中一個或多個資料行相關聯的許可權清單。|  
|**SQLProcedures**|傳回資料來源中的程式清單。|  
|**SQLProcedureColumns**|傳回單一程式之結果集中的輸入和輸出參數、傳回值和資料行的清單。|  
|**SQLGetTypeInfo**|傳回資料來源所支援的 SQL 資料類型清單。 這些資料類型通常用於**CREATE TABLE**和**ALTER TABLE**語句中。|  
  
 因為**SQLTables**、 **SQLColumns**、 **SQLStatistics**和**SQLSpecialColumns**符合開放式群組 cli，而**SQLGetTypeInfo**符合 ISO 92 cli，所以它們是由大部分的驅動程式所執行。 其餘的目錄函數會在 ODBC 一致性層級中。  
  
 此章節包含下列主題。  
  
-   [目錄函式所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [目錄函式中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [結構描述檢視](../../../odbc/reference/develop-app/schema-views.md)
