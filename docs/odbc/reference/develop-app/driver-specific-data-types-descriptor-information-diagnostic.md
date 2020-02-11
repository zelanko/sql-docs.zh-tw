---
title: 驅動程式特有的類型-資料、描述元、資訊、診斷 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa17a5552855916798c78e0e7d371b58e58a401e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046925"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>特定驅動程式的資料類型、描述項類型、資訊類型、診斷類型與屬性
驅動程式可以為下列各項配置驅動程式特定的值：  
  
-   **SQL 資料類型指示器**這些會用於**SQLBindParameter**中的*ParameterType*和**SQLGetTypeInfo**中的*DataType* ，並由**SQLColAttribute**、 **SQLColumns**、 **SQLDescribeCol**、 **SQLGetTypeInfo**、 **SQLDescribeParam**、 **SQLProcedureColumns**和**SQLSpecialColumns**傳回。  
  
-   **描述項欄位**這些是在**SQLColAttribute**、 **SQLGetDescField**和**SQLSetDescField**的*FieldIdentifier*中使用。  
  
-   **診斷欄位**這些是在**SQLGetDiagField**和**SQLGetDiagRec**的*以*中使用。  
  
-   **資訊類型**這些是在**SQLGetInfo**的*InfoType*中使用。  
  
-   **Connection 和語句屬性**這些是在**SQLGetConnectAttr**、 **SQLGetStmtAttr**、 **SQLSetConnectAttr**和**SQLSetStmtAttr**的*屬性*中使用。  
  
 每個專案都有兩組值：保留供 ODBC 使用的值，以及保留供驅動程式使用的值。 在執行驅動程式特有的值之前，驅動程式寫入器必須向 Open Group 中的每個驅動程式特定類型、欄位或屬性要求一個值。 針對新的驅動程式開發，請使用下表所述的範圍。 如果使用的未知值不在下方描述的範圍中，ODBC 3.8 驅動程式管理員將不會產生錯誤。 不過，如果收到的未知值不在範圍內，較新版本的驅動程式管理員可能會產生錯誤。  
  
 當任何一個值傳遞至 ODBC 函數時，驅動程式必須檢查值是否有效。 驅動程式會傳回適用于其他驅動程式之驅動程式特定值的 SQLSTATE HYC00 （未執行的選擇性功能）。  
  
 從 ODBC 3.8 開始，驅動程式寫入器可以在保留的範圍內配置驅動程式特有的屬性。  
  
> [!NOTE]  
>  ODBC 3.8 驅動程式管理員不會針對回溯相容性進行驗證，也不會強制執行這些範圍。 不過，未來的驅動程式管理員版本可能會強制執行它們。  
  
|屬性類型|ODBC 資料類型|驅動程式特定的範圍基底|驅動程式特定範圍限制|驅動程式特定值範圍基底的 ODBC 常數|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL 資料類型指示器|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|描述項欄位|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|診斷欄位|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|資訊類型|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|連接屬性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|語句屬性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  驅動程式特有的資料類型、描述項欄位、診斷欄位、資訊類型、語句屬性和連接屬性，都必須在驅動程式檔中說明。 當任何一個值傳遞至 ODBC 函數時，驅動程式必須檢查值是否有效。 驅動程式會傳回適用于其他驅動程式之驅動程式特定值的 SQLSTATE HYC00 （未執行的選擇性功能）。  
  
 系統會定義基底值，以加速驅動程式開發。 例如，您可以用下列格式來定義驅動程式特定的診斷屬性：  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
