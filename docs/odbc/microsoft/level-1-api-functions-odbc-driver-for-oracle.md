---
title: 1 級 API 功能(Oracle 的 ODBC 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37305ee75ebeb0686bafe039f1102cb3c6e18674
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299948"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>層級 1 API 函式 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 此級別的功能提供核心介面一致性以及其他功能(如事務支援)。  
  
|API 功能|注意|  
|------------------|-----------|  
|**SQLColumns**|為表創建結果集,該表是指定表或表的列清單。 請求 PUBLIC 同義詞的列時,必須設置 SYNONYMCOLUMNS 連接屬性,並將空字串指定為*szTableOwner*參數。 傳回 PUBLIC 同義字的欄時,驅動程式將 TABLE NAME 列設定為空字串。 結果集在每行末尾包含一個附加列"ORDINAL 位置"。 此值是表中列的正位位置。|  
|**SQLDriverConnect**|連接到現有數據源。 關於詳細資訊,請參考[連接字串格式與屬性](../../odbc/microsoft/connection-string-format-and-attributes.md)。|  
|**SQLGetConnectOption**|傳回連接選項的當前設置。 此函數部分受支援。 驅動程式支援*fOption*參數的所有值,但不支援*fOption*參數[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)的某些*vParam*值。 有關詳細資訊,請參閱[連線選項](../../odbc/microsoft/connect-options.md)。|  
|**SQLGetData**|檢索給定結果集的當前記錄中單個字段的值。|  
|**SQLGetFunctions**|為所有支援的函數返回 TRUE。 由驅動程式管理員實施。|  
|**SQLGetInfo**|返回有關 Oracle 的 ODBC 驅動程式以及\*與連接句柄*hdbc*關聯的資料來源的資訊,包括 SQLHDBC、SQLUSMALLINT、SQLPOINTER、SQLSMALLINT 和 SQLSMALLINT。|  
|**SQLGetStmtOption**|返回語句選項的當前設置。 有關詳細資訊,請參閱[敘述選項](../../odbc/microsoft/statement-options.md)。|  
|**SQLGetTypeInfo**|返回有關數據源支援的數據類型的資訊。 驅動程式返回 SQL 結果集中的資訊。|  
|**SQLParamData**|與**SQLPutData**結合使用,在語句執行時指定參數數據。|  
|**SQLPutData**|允許應用程式在語句執行時將參數或列的數據發送到驅動程式。|  
|**SQLSet 連線選項**|提供對管理連接各個方面的選項的訪問。 此函數部分支援:驅動程式支援*fOption*參數的所有值,但不支援*fOption*參數[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)的某些*vParam*值。 有關詳細資訊,請參閱[連線選項](../../odbc/microsoft/connect-options.md)。|  
|**SQLSetStmtOption**|設置與語句句柄*hstmt*相關的選項。 有關詳細資訊,請參閱[敘述選項](../../odbc/microsoft/statement-options.md)。|  
|**SQLSpecialColumns**|檢索唯一標識表中行的最佳列集。|  
|**SQLStatistics**|檢索有關單個表以及與表關聯的索引或標記名稱的統計資訊清單。 驅動程式將返回結果集。|  
|**SQLTables**|傳回**SQLTables**敘述中參數指定的表格名稱的清單。 如果未指定參數,則返回存儲在當前數據源中的表名稱。 驅動程式將返回結果集。<br /><br /> 枚舉類型調用將不會接收遠端檢視或本地參數化檢視的結果集條目。 但是,對**SQLTables**的調用具有唯一的表名稱指定器,將查找具有該名稱的此類視圖的匹配項(如果存在);這允許 API 在創建新表之前檢查名稱衝突。<br /><br /> 公共同義詞返回時,值為"TABLE_OWNER。<br /><br /> SYS 或 SYSTEM 擁有的檢視標識為系統檢視。|
