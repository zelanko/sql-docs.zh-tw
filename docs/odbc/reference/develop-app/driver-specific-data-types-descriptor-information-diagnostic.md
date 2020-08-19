---
description: 特定驅動程式的資料類型、描述項類型、資訊類型、診斷類型與屬性
title: 驅動程式特定類型-資料、描述元、資訊、診斷 |Microsoft Docs
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
ms.openlocfilehash: 9a0ac3fd67e07f23f14420ee46ccda5cd409f87a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483001"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>特定驅動程式的資料類型、描述項類型、資訊類型、診斷類型與屬性
驅動程式可以針對下列各項配置驅動程式特定的值：  
  
-   **SQL 資料類型**指標這些會在**SQLBindParameter**和**SQLGetTypeInfo** *中的* *ParameterType*中使用，並由**SQLColAttribute**、 **SQLColumns**、 **SQLDescribeCol**、 **SQLGetTypeInfo**、 **SQLDescribeParam**、 **SQLProcedureColumns**和**SQLSpecialColumns**所傳回。  
  
-   **描述項欄位**這些會在**SQLColAttribute**、 **SQLGetDescField**和**SQLSetDescField**的*FieldIdentifier*中使用。  
  
-   **診斷欄位**這些是在**SQLGetDiagField**和**SQLGetDiagRec**的*以*中使用。  
  
-   **資訊類型**這些會在**SQLGetInfo**的*InfoType*中使用。  
  
-   **Connection 和語句屬性**這些會在**SQLGetConnectAttr**、 **SQLGetStmtAttr**、 **SQLSetConnectAttr**和**SQLSetStmtAttr**的*屬性*中使用。  
  
 每個專案都有兩個值集合：保留供 ODBC 使用的值，以及保留供驅動程式使用的值。 在執行驅動程式特定的值之前，驅動程式寫入器必須針對每個驅動程式特定的類型、欄位或開啟的群組中的屬性要求一個值。 針對新的驅動程式開發，請使用下表所述的範圍。 如果使用的未知值不在以下所述的範圍中，ODBC 3.8 驅動程式管理員將不會產生錯誤。 但是，如果接收到的未知值不在範圍內，則較新版本的驅動程式管理員可能會產生錯誤。  
  
 當這些值的任何一個傳遞到 ODBC 函數時，驅動程式必須檢查值是否有效。 驅動程式會傳回 SQLSTATE HYC00 (未針對套用至其他驅動程式的驅動程式特定值) 執行的選用功能。  
  
 從 ODBC 3.8 開始，驅動程式寫入器可以在保留範圍內配置驅動程式特有的屬性。  
  
> [!NOTE]  
>  ODBC 3.8 驅動程式管理員不會針對回溯相容性驗證或強制執行這些範圍。 但是，驅動程式管理員的未來版本可能會強制執行。  
  
|屬性類型|ODBC 資料類型|驅動程式特定的範圍基底|驅動程式特定的範圍限制|驅動程式專用值範圍基底的 ODBC 常數|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL 資料類型指標|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|描述項欄位|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|診斷欄位|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|資訊類型|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|連接屬性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|語句屬性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  驅動程式特定的資料類型、描述項欄位、診斷欄位、資訊類型、語句屬性和連接屬性，都必須在驅動程式檔中說明。 當這些值的任何一個傳遞到 ODBC 函數時，驅動程式必須檢查值是否有效。 驅動程式會傳回 SQLSTATE HYC00 (未針對套用至其他驅動程式的驅動程式特定值) 執行的選用功能。  
  
 定義基底值以促進驅動程式開發。 例如，您可以用下列格式來定義驅動程式特定的診斷屬性：  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
