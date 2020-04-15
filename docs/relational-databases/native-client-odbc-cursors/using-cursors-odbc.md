---
title: 使用游標 (ODBC) |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC]
- ODBC cursors
ms.assetid: 51322f92-0d76-44c9-9c33-9223676cf1d3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: be512713462a9518856de2a16db749490ea24366
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306278"
---
# <a name="using-cursors-odbc"></a>使用資料指標 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 支援的資料指標模型允許：  
  
-   數種資料指標類型。  
  
-   在資料指標內捲動和定位。  
  
-   多個並行選項。  
  
-   定位更新。  
  
 ODBC 應用程式很少會宣告及開啟資料指標，或使用任何與資料指標相關的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 ODBC 會針對每個從 SQL 陳述式傳回的結果集而自動開啟資料指標。 在執行 SQL 語句之前,游標的特徵由使用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)設置的語句屬性控制。 用來處理結果集的 ODBC API 函數支援完整的資料指標功能，包括提取、捲動和定位更新等。  
  
 這是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼和 ODBC 應用程式如何搭配資料指標使用的比較。  
  
|動作|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBC|  
|------------|------------------------|----------|  
|定義資料指標行為|指定透過 DECLARE CURSOR 參數|使用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)設定游標屬性|  
|開啟資料指標|宣告游標開啟*cursor_name*|**SQLExecDirect**或**SQLExecute**|  
|提取資料列|FETCH|**SQLFetch**或[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)|  
|定點更新|UPDATE 或 DELETE 上的 WHERE CURRENT OF 子句|**SQLSetPos**|  
|關閉資料指標|關閉*cursor_name*取消配置|[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)|  
  
 實作於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的伺服器資料指標支援 ODBC 資料指標模型的功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 驅動程式使用伺服器資料指標支援 ODBC API 的資料指標功能。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [如何實作資料指標](../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
-   [資料指標類型](../../relational-databases/native-client-odbc-cursors/cursor-types.md)  
  
-   [資料指標行為](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
-   [資料指標屬性](../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
-   [游標程式設計詳細資訊&#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
-   [捲動與提取資料列](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
-   [定位更新&#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/positioned-updates-odbc.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL 伺服器本機用戶端&#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [關閉&#40;交易-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [游標](../../relational-databases/cursors.md)   
 [&#40;转算-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [聲明&#40;轉算-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [獲取&#40;轉接-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
