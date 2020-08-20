---
description: 資料類型使用方式
title: 資料類型使用方式 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data types
- ODBC data types, about ODBC data types
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC]
- SQL Server Native Client ODBC driver, data types
- data types [ODBC], about data types
ms.assetid: 4f19b0d6-94ac-4a98-a121-57d38787864c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4a2e5fce7a76c22ac89f324cc69010311ab01883
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465371"
---
# <a name="data-type-usage"></a>資料類型使用方式
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 ODBC 驅動程式會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 強制使用下列資料類型。  
  
|資料類型|限制|  
|---------------|----------------|  
|日期常值|當日期常值儲存于 SQL_TYPE_TIMESTAMP 資料行 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 或 **Smalldatetime**) 的資料類型時，其時間值為12：00： 00.000 A.M。|  
|**money** 和 **smallmoney**|只有 **money** 和 **smallmoney** 資料類型的整數部分是很重要的。 如果在資料類型轉換期間截斷 SQL **money** 資料的小數部分，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會傳回警告，而非錯誤。|  
|SQL_BINARY (可為 Null)|連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 版和更早版本時，如果 SQL_BINARY 資料行可為 Null，則儲存在資料來源中的資料就不會以零進行填補。 當抓取這類資料行的資料時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會在右邊以零填補。 不過，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所執行的作業 (例如串連) 中建立的資料就沒有此類填補。<br /><br /> 此外，當資料是放在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 或更早版本之執行個體的此類資料行中，且資料太長而無法放入資料行時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會從右側截斷資料。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式支援連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 及更早版本。|  
|SQL_CHAR (截斷)|如果是連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本的執行個體，而且資料是放在 SQL_CHAR 資料行中，則在資料太長無法放入資料行時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在未提供警告的情況下從右側截斷資料。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式支援連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 及更早版本。|  
|SQL_CHAR (可為 Null)|當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本時，如果 SQL_CHAR 資料行可為 Null，則儲存在資料來源中的資料就不會以空白進行填補。 當抓取來自這類資料行的資料時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會將右邊的空格填補。 不過，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所執行的作業 (例如串連) 中建立的資料就沒有此類填補。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式支援連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 及更早版本。|  
|SQL_LONGVARBINARY、SQL_LONGVARCHAR、SQL_WLONGVARCHAR|當連接到6的實例時，會完全支援使用 WHERE 子句) SQL_LONGVARBINARY、SQL_LONGVARCHAR 或 SQL_WLONGVARCHAR 資料 (類型的資料行更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。*x* 和更新版本。 連接到 4.2 x 的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時*x*，會發生 S1000 錯誤：「部分插入/更新。 文字或影像資料行的插入/更新未成功」。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式支援連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 及更早版本。|  
|字串函數參數|字串函數的*string_exp*參數必須是 SQL_CHAR 或 SQL_VARCHAR 的資料類型。 字串函數中不支援 SQL_LONG_VARCHAR 資料類型。 *Count*參數必須小於或等於8000，因為 SQL_CHAR 和 SQL_VARCHAR 資料類型受限於8000個字元的最大長度。|  
|時間常值|當時間常值儲存在 SQL_TIMESTAMP 資料行 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 或 **Smalldatetime**) 的資料類型時，其日期值為1900年1月1日。|  
|**timestamp**|只能以手動方式將 Null 值插入 **時間戳記** 資料行。 不過，因為 **時間戳記**資料行是由自動更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，所以會覆寫 Null 值。|  
|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Tinyint**資料類型不帶正負號。 **Tinyint**資料行預設會系結至資料類型 SQL_C_UTINYINT 的變數。|  
|別名資料類型|當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4.2*x*的實例時，ODBC 驅動程式會將 Null 加入至未明確宣告資料行 null 屬性的資料行定義。 因此會忽略儲存在別名資料類型定義中的 Null 屬性。<br /><br /> 連接到 4.2 x 的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時*x*，具有別名資料類型的資料行具有**char**或**binary**的基底資料類型，而且沒有宣告 null 屬性的資料行，會建立為**Varchar**或**Varbinary**資料類型。 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)、 [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)和 [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 會傳回 SQL_VARCHAR 或 SQL_VARBINARY 作為這些資料行的資料類型。 從這些資料行所擷取的資料不會進行填補。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式支援連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 及更早版本。|  
|LONG 資料類型|SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 資料類型都限制*資料執行中*參數。|  
|大型值類型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 ODBC 驅動程式會在接受或傳回 ODBC SQL 資料類型的 api 中，分別公開**Varchar (max) **、 **Varbinary (max) **和**Nvarchar (max) **類型 SQL_VARCHAR SQL_VARBINARY、SQL_WVARCHAR 和 () 。|  
|使用者定義型別 (UDT)|UDT 資料行會對應為 SQL_SS_UDT。 如果 UDT 資料行使用 UDT 的 ToString() 或 ToXMLString() 方法或是透過 CAST/CONVERT 函數而明確地對應到 SQL 陳述式中的其他類型，則結果集內的資料行類型會反映出此資料行轉換成的實際類型。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式只能以二進位格式系結至 UDT 資料行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只支援 SQL_SS_UDT 和 SQL_C_BINARY 資料類型之間的轉換。|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動將 XML 轉換為 Unicode 文字。 XML 類型會對應為 SQL_SS_XML。|  
  
## <a name="see-also"></a>另請參閱  
 [處理 &#40;ODBC&#41;的結果 ](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
