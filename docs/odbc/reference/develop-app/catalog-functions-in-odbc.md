---
title: 目錄在 ODBC 中的函式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8cd46fbc8f633ef31f00fa60ced885f9455f185
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062736"
---
# <a name="catalog-functions-in-odbc"></a>ODBC 中的目錄函式
ODBC 會包含下列目錄函式：  
  
|函數|描述|  
|--------------|-----------------|  
|**SQLTables**|傳回資料來源中的目錄、 結構描述、 資料表或資料表類型的清單。|  
|**SQLColumns**|傳回一或多個資料表中的資料行的清單。|  
|**SQLStatistics**|傳回單一資料表的相關統計資料的清單。 也會傳回一份與該資料表相關聯的索引。|  
|**SQLSpecialColumns**|傳回可唯一識別單一資料表中的資料列的資料行清單。 也會自動更新該資料表中傳回資料行的清單。|  
|**SQLPrimaryKeys**|傳回組成單一資料表的主索引鍵資料行的清單。|  
|**SQLForeignKeys**|傳回單一資料表或在單一資料表參考其他資料表中的外部索引鍵的清單中的外部索引鍵的清單。|  
|**SQLTablePrivileges**|傳回與一或多個資料表相關聯的權限的清單。|  
|**SQLColumnPrivileges**|傳回單一資料表中的一或多個資料行相關聯的權限的清單。|  
|**SQLProcedures**|傳回資料來源中的程序的清單。|  
|**SQLProcedureColumns**|在單一程序的結果集傳回輸入和輸出參數、 傳回值和資料行的清單。|  
|**SQLGetTypeInfo**|傳回資料來源所支援的 SQL 資料類型的清單。 這些資料型別通常用於**CREATE TABLE**並**ALTER TABLE**陳述式。|  
  
 因為**SQLTables**， **SQLColumns**， **SQLStatistics**，以及**SQLSpecialColumns**符合開啟群組 CLI，以及**SQLGetTypeInfo**符合 ISO 92 CLI，它們在實作大部分的驅動程式。 其餘的類別目錄函式位於 ODBC 的一致性層級。  
  
 此章節包含下列主題。  
  
-   [目錄函式所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [目錄函式中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [結構描述檢視](../../../odbc/reference/develop-app/schema-views.md)
