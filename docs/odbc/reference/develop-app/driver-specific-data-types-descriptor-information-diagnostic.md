---
title: 特定於驅動程式的類型 - 資料、描述符、資訊、診斷 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19bb2dd113fbeae871892ea510713c638c886e5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305761"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>特定驅動程式的資料類型、描述項類型、資訊類型、診斷類型與屬性
驅動程式可以為以下分配特定於驅動程式的值:  
  
-   **SQL 資料型態指示器**這些在**SQLBind 參數**中的*參數類型*和**SQLGetTypeInfo**中的*資料類型*中使用,並由**SQLCol 屬性**、SQL、SqlDescribeCol、SQLGetTypeinfo、SQL**描述列****、SQL程式列**和**SQL 特殊列**返回。 **SQLColumns** **SQLDescribeCol** **SQLGetTypeInfo**  
  
-   **描述字欄位**這些用於**在 SQLColattribute、SQLGetDescField**和**SQLSetDescField**中的*字段識別碼*中。 **SQLGetDescField**  
  
-   **診斷欄位**這些在**SQLGetDiagField**與**SQLGetDiagRec**中用於*Diag 識別碼*。  
  
-   **資訊類型**這些在**SQLGetInfo**中的*資訊類型*中使用。  
  
-   **連接與敘述屬性**這些在**SQLGetConnect Attr、SQLGetStmtAttr、SQLSetConnectAttr**和*Attribute***SQLSetStmtAttr**中使用。 **SQLGetStmtAttr** **SQLSetConnectAttr**  
  
 對於每個專案,有兩組值:為 ODBC 保留的值,以及保留供驅動程式使用的值。 在實現特定於驅動程式的值之前,驅動程式編寫器必須請求 Open Group 中每個特定於驅動程式的類型、欄位或屬性的值。 對於新的驅動程式開發,請使用下表中描述的範圍。 如果使用的未知值不在下面描述的範圍內,ODBC 3.8 驅動程式管理器不會生成錯誤。 但是,如果收到不在範圍中的未知值,則驅動程式管理器的更高版本可能會生成錯誤。  
  
 當這些值中的任何一個傳遞給 ODBC 函數時,驅動程式必須檢查該值是否有效。 驅動程式返回 SQLSTATE HYC00(未實現可選功能)以執行適用於其他驅動程式的特定於驅動程式的值。  
  
 從 ODBC 3.8 開始,驅動程式編寫器可以在保留範圍內分配特定於驅動程式的屬性。  
  
> [!NOTE]  
>  ODBC 3.8 驅動程式管理員既不驗證也不強制這些範圍的向後相容性。 但是,驅動程式管理器的未來版本可能會強制執行它們。  
  
|屬性類型|ODBC 資料類型|特定於驅動程式的範圍底座|特定於驅動程式的範圍限制|特定於驅動程式的值範圍基礎的 ODBC 常量|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL 資料型態指示器|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|描述字欄位|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|診斷欄位|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|資訊類型|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|連線屬性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|語句屬性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  驅動程式文件中必須描述特定於驅動程式的數據類型、描述符欄位、診斷欄位、資訊類型、語句屬性和連接屬性。 當這些值中的任何一個傳遞給 ODBC 函數時,驅動程式必須檢查該值是否有效。 驅動程式返回 SQLSTATE HYC00(未實現可選功能)以執行適用於其他驅動程式的特定於驅動程式的值。  
  
 定義基值是為了促進驅動程序的開發。 例如,驅動程式特定的診斷屬性可以定義以下格式:  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
