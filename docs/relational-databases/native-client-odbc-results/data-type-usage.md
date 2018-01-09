---
title: "資料類型使用方式 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-results
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 385a12cb44b6f9a6841e1480035edd3de7ee8e59
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="data-type-usage"></a>資料類型使用方式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]下列用法的資料類型。  
  
|資料類型|限制|  
|---------------|----------------|  
|日期常值|儲存於 SQL_TYPE_TIMESTAMP 資料行的日期常值 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別**datetime**或**smalldatetime**)，有 12:00:00.000 A.M.的時間值|  
|**money**和**smallmoney**|只有整數部分的**money**和**smallmoney**資料型別是有意義。 如果 SQL 的小數部分**money**進行資料類型轉換時，會截斷資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會傳回警告，而不是錯誤。|  
|SQL_BINARY (可為 Null)|連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 版和更早版本時，如果 SQL_BINARY 資料行可為 Null，則儲存在資料來源中的資料就不會以零進行填補。 從這類資料行的資料擷取時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式在右邊的零進行填補。 不過，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所執行的作業 (例如串連) 中建立的資料就沒有此類填補。<br /><br /> 此外，當資料是放在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 或更早版本之執行個體的此類資料行中，且資料太長而無法放入資料行時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會從右側截斷資料。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 及更早版本。|  
|SQL_CHAR (截斷)|如果是連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本的執行個體，而且資料是放在 SQL_CHAR 資料行中，則在資料太長無法放入資料行時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在未提供警告的情況下從右側截斷資料。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 及更早版本。|  
|SQL_CHAR (可為 Null)|當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本時，如果 SQL_CHAR 資料行可為 Null，則儲存在資料來源中的資料就不會以空白進行填補。 從這類資料行的資料擷取時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式以在右邊的空白進行填補。 不過，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所執行的作業 (例如串連) 中建立的資料就沒有此類填補。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 及更早版本。|  
|SQL_LONGVARBINARY、SQL_LONGVARCHAR、SQL_WLONGVARCHAR|連接到的執行個體時，完全支援 SQL_LONGVARBINARY、 SQL_LONGVARCHAR 或 SQL_WLONGVARCHAR 資料類型資料行 （使用 WHERE 子句） 會影響多個資料列的更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6。*x*和更新版本。 當連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4.2*x*，就會傳回 S1000 錯誤，「 部分插入/更新。 文字或影像資料行的插入/更新未成功」。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 及更早版本。|  
|字串函數參數|*string_exp* SQL_CHAR 或 SQL_VARCHAR，輸入參數的資料必須是函式的字串。 字串函數中不支援 SQL_LONG_VARCHAR 資料類型。 *計數*參數必須是小於或等於 8,000 因為 SQL_CHAR 和 SQL_VARCHAR 資料類型是有限的最大長度為 8,000 個字元。|  
|時間常值|時間常值，當儲存於 SQL_TYPE_TIMESTAMP 資料行 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別**datetime**或**smalldatetime**)，有 1900 年 1 月 1 日的日期值。|  
|**timestamp**|只有 NULL 值以手動方式插入至**時間戳記**資料行。 不過，因為**時間戳記**資料行所自動更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，NULL 值會覆寫。|  
|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Tinyint**資料類型是不帶正負號。 A **tinyint**資料行繫結到 SQL_C_UTINYINT 資料類型的變數預設值。|  
|別名資料類型|當連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4.2*x*，ODBC 驅動程式會將 NULL 加入至資料行定義中，未明確宣告資料行的 null 屬性。 因此會忽略儲存在別名資料類型定義中的 Null 屬性。<br /><br /> 當連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4.2*x*，具有別名資料類型具有基底資料的資料行類型**char**或**二進位**並沒有 null 屬性是宣告會建立資料類型為**varchar**或**varbinary**。 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)， [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)，和[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)傳回 SQL_VARCHAR 或 SQL_VARBINARY 當做資料輸入這些資料行。 從這些資料行所擷取的資料不會進行填補。<br /><br /> 注意： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 及更早版本。|  
|LONG 資料類型|*資料在執行*參數則都限制為 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 資料類型。|  
|大型值類型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會公開**varchar （max)**， **varbinary （max)**，和**nvarchar （max)**為 SQL_VARCHAR、 SQL_VARBINARY 和 SQL_ 類型WVARCHAR （分別） 在應用程式開發介面，接受或傳回 ODBC SQL 資料類型。|  
|使用者定義型別 (UDT)|UDT 資料行會對應為 SQL_SS_UDT。 如果 UDT 資料行使用 UDT 的 ToString() 或 ToXMLString() 方法或是透過 CAST/CONVERT 函數而明確地對應到 SQL 陳述式中的其他類型，則結果集內的資料行類型會反映出此資料行轉換成的實際類型。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式只能繫結到 UDT 資料行，為二進位。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只支援 SQL_SS_UDT 和 SQL_C_BINARY 資料類型之間的轉換。|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動將 XML 轉換為 Unicode 文字。 XML 類型會對應為 SQL_SS_XML。|  
  
## <a name="see-also"></a>請參閱  
 [處理結果 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
