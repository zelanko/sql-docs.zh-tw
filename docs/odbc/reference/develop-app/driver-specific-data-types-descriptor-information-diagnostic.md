---
title: "驅動程式特定類型的資料，描述元的詳細資訊，診斷 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 05aaeca12342ec9d037595ff001a0d1edc745818
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>驅動程式特定資料類型、 描述元類型、 資訊類型、 診斷的型別和屬性
驅動程式可以針對下列配置驅動程式專屬的值：  
  
-   **SQL 資料類型的指標**中會使用這些*ParameterType*中**SQLBindParameter**和*DataType*中**SQLGetTypeInfo** ，並由傳回**SQLColAttribute**， **SQLColumns**， **SQLDescribeCol**， **SQLGetTypeInfo**， **SQLDescribeParam**， **SQLProcedureColumns**，和**SQLSpecialColumns**。  
  
-   **描述項欄位**中會使用這些*FieldIdentifier*中**SQLColAttribute**， **SQLGetDescField**，和**SQLSetDescField**.  
  
-   **診斷欄位**中會使用這些*Sqlgetdiagfield*中**SQLGetDiagField**和**SQLGetDiagRec**。  
  
-   **資訊類型**中會使用這些*資訊類型*中**SQLGetInfo**。  
  
-   **連接和陳述式屬性**中會使用這些*屬性*中**SQLGetConnectAttr**， **SQLGetStmtAttr**， **SQLSetConnectAttr**，和**SQLSetStmtAttr**。  
  
 針對每個這些項目中，有兩組值： 保留供 ODBC、 值和保留供驅動程式的值。 在實作之前驅動程式專屬的值，驅動程式撰寫者必須從 Open Group 要求每個驅動程式專屬的型別、 欄位或屬性的值。 新的驅動程式開發，使用下表中所述的範圍。 如果未知的值不在範圍內，如下所述，使用 ODBC 3.8 驅動程式管理員不會產生錯誤。 不過，較新版本的驅動程式管理員可能會產生錯誤，如果收到不在範圍內的未知的值。  
  
 當這些值傳遞給 ODBC 函數時，驅動程式必須檢查值是否有效。 驅動程式傳回 SQLSTATE HYC00 （未實作的選擇性功能） 適用於其他驅動程式的驅動程式專屬值。  
  
 開始使用 ODBC 3.8，驅動程式寫入器可以配置的保留範圍內的驅動程式專屬屬性。  
  
> [!NOTE]  
>  ODBC 3.8 驅動程式管理員不會驗證也不會強制執行這些範圍回溯相容性上。 未來版本的驅動程式管理員可能會強制套用它們，不過。  
  
|屬性類型|ODBC 資料類型|基底的驅動程式專屬範圍|驅動程式專屬範圍限制|ODBC 驅動程式專屬數值範圍基底的常數|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL 資料類型的指標|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|描述項欄位|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|診斷欄位|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|資訊類型|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|連接屬性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|陳述式屬性|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  驅動程式文件必須描述驅動程式特定資料類型，描述項欄位、 診斷欄位、 資訊類型、 陳述式屬性和連接屬性。 當這些值傳遞給 ODBC 函數時，驅動程式必須檢查值是否有效。 驅動程式傳回 SQLSTATE HYC00 （未實作的選擇性功能） 適用於其他驅動程式的驅動程式專屬值。  
  
 若要協助驅動程式開發定義基底值。 例如，驅動程式特定的診斷屬性可以定義格式如下：  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```

