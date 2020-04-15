---
title: 資料類型使用方式 |微軟文件
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
ms.openlocfilehash: 0384857c53e898af9fca89bb2ee2351f0b65f986
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297852"
---
# <a name="data-type-usage"></a>資料類型使用方式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 ODBC[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驅動程式 ,並強制使用以下數據類型。  
  
|資料類型|限制|  
|---------------|----------------|  
|日期常值|日期文字,當儲存在SQL_TYPE_TIMESTAMP列([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**日期時間**或**小日期時間的**數據類型)時,時間值為上午 12:00:00.000。|  
|**錢****和小錢**|只有**貨幣**和小**貨幣**數據類型的整數部分才顯著。 如果在資料類型轉換期間截斷 SQL**貨幣**資料的十進位[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]部分, 本機用戶端 ODBC 驅動程式將傳回警告,而不是錯誤。|  
|SQL_BINARY (可為 Null)|連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 版和更早版本時，如果 SQL_BINARY 資料行可為 Null，則儲存在資料來源中的資料就不會以零進行填補。 檢索此類列中的數據時,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式將右側的零填充。 不過，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所執行的作業 (例如串連) 中建立的資料就沒有此類填補。<br /><br /> 此外，當資料是放在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 或更早版本之執行個體的此類資料行中，且資料太長而無法放入資料行時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會從右側截斷資料。<br /><br /> 注意:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式確實[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援連接到 6.5 和更早版本。|  
|SQL_CHAR (截斷)|如果是連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本的執行個體，而且資料是放在 SQL_CHAR 資料行中，則在資料太長無法放入資料行時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在未提供警告的情況下從右側截斷資料。<br /><br /> 注意:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式確實[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援連接到 6.5 和更早版本。|  
|SQL_CHAR (可為 Null)|當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 和更早版本時，如果 SQL_CHAR 資料行可為 Null，則儲存在資料來源中的資料就不會以空白進行填補。 檢索此類列中的資料時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 本機客戶端 ODBC 驅動程式會用右側的空白填充數據。 不過，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所執行的作業 (例如串連) 中建立的資料就沒有此類填補。<br /><br /> 注意:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式確實[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援連接到 6.5 和更早版本。|  
|SQL_LONGVARBINARY、SQL_LONGVARCHAR、SQL_WLONGVARCHAR|連接到 6 的實例時,完全支援使用SQL_LONGVARBINARY、SQL_LONGVARCHAR或SQL_WLONGVARCHAR數據類型(使用 WHERE 子句)[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]影響多個行的 列的更新。*x*及更高版本。 當連接到實例 4.2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *x*時,S1000 錯誤「部分插入/更新」。。 文字或影像資料行的插入/更新未成功」。<br /><br /> 注意:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式確實[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援連接到 6.5 和更早版本。|  
|字串函數參數|*字串函數的string_exp*參數必須是數據類型SQL_CHAR或SQL_VARCHAR。 字串函數中不支援 SQL_LONG_VARCHAR 資料類型。 *計數*參數必須小於或等於 8,000,因為SQL_CHAR和SQL_VARCHAR數據類型限制為 8,000 個字元的最大長度。|  
|時間常值|時間文字,當儲存在SQL_TIMESTAMP列([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**日期時間**或**小日期時間的**資料類型)的日期值為 1900 年 1 月 1 日。|  
|**時間 戳**|只能手動將 NULL 值插入**時間戳**列。 但是,由於**時間戳**列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]由自動更新,因此將覆蓋 NULL 值。|  
|**小金特**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**小字體**數據類型是無符號的。 默認情況下 **,小列**綁定到數據類型的變數SQL_C_UTINYINT。|  
|別名資料類型|當連接到 4.2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *x*的實例時,ODBC 驅動程式將 NULL 添加到不顯式聲明列的 null 的列定義。 因此會忽略儲存在別名資料類型定義中的 Null 屬性。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當連線到 4.2*x*的實體時,具有別名資料類型的欄位有**字元**或**二進位**的的基本資料類型,並且不聲明 null,則建立為資料類型**varchar**或**varbinary**。 [SQLColAttribute、SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)[SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)和[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)返回SQL_VARCHAR或SQL_VARBINARY作為這些列的數據類型。 從這些資料行所擷取的資料不會進行填補。<br /><br /> 注意:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式確實[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援連接到 6.5 和更早版本。|  
|LONG 資料類型|*對於*SQL_LONGVARBINARY和SQL_LONGVARCHAR數據類型,執行時的數據參數都受到限制。|  
|大型值類型|本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 ODBC 驅動程式將在接受或返回 ODBC SQL 資料類型的 API 中公開**varchar(最大值****)、varbinary(max)** 和**nvarchar(max)** 類型,作為 SQL_VARCHAR、SQL_VARBINARY和SQL_WVARCHAR(分別為)。|  
|使用者定義型別 (UDT)|UDT 資料行會對應為 SQL_SS_UDT。 如果 UDT 資料行使用 UDT 的 ToString() 或 ToXMLString() 方法或是透過 CAST/CONVERT 函數而明確地對應到 SQL 陳述式中的其他類型，則結果集內的資料行類型會反映出此資料行轉換成的實際類型。<br /><br /> 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 ODBC 驅動程式只能綁定到 UDT 列作為二進位。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只支援 SQL_SS_UDT 和 SQL_C_BINARY 資料類型之間的轉換。|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動將 XML 轉換為 Unicode 文字。 XML 類型會對應為 SQL_SS_XML。|  
  
## <a name="see-also"></a>另請參閱  
 [處理結果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
