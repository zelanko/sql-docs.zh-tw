---
title: 執行查詢 (ODBC) |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, executing queries
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
- SQL Server Native Client ODBC driver, queries
- queries [ODBC]
ms.assetid: d935bcba-8ce6-4159-8395-6c86431602ad
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93984308c9b661af8e7263ed1c3c0a54e1b35eab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297992"
---
# <a name="executing-queries-odbc"></a>執行查詢 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  當 ODBC 應用程式將連接控制代碼初始化並連接資料來源後，會在連接控制代碼上配置一個或多個陳述式控制代碼。 然後,應用程式可以在語句[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]句柄上執行語句。 執行 SQL 陳述式的一般事件序列是：  
  
1.  設定任何需要的陳述式屬性。  
  
2.  建構陳述式。  
  
3.  執行陳述式。  
  
4.  擷取任何結果集。  
  
 當應用程式擷取在 (由 SQL 陳述式傳回的) 所有結果集的資料列後，可以在相同陳述式控制代碼上執行另一個查詢。 如果應用程式確定不需要檢索特定結果集中的所有行,則可以通過調用[SQLMoreResult](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)或[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)來取消結果集的其餘部分。  
  
 在 ODBC 應用程式中，如果您必須用不同資料多次執行相同的 SQL 陳述式，則在 SQL 陳述式的建構中使用由問號 (?) 所代表的參數標記：  
  
```  
INSERT INTO MyTable VALUES (?, ?, ?)  
```  
  
 然後,通過調用[SQLBind 參數](../../relational-databases/native-client-odbc-api/sqlbindparameter.md),可以將每個參數標記綁定到程式變數。  
  
 在執行所有 SQL 陳述式，而且也處理其結果集之後，應用程式會釋放陳述式控制代碼。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 ODBC 驅動程式支援每個連接句柄的多個語句句柄。 由於交易是在連接層級管理，因此在所有陳述式控制代碼上所執行的所有工作，會在單一連接控制代碼上管理成為相同交易的一部分。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [配置陳述式控制代碼](../../relational-databases/native-client-odbc-queries/allocating-a-statement-handle.md)  
  
-   [建構 &#40;ODBC&#41;的 SQL 語句](../../relational-databases/native-client-odbc-queries/constructing-an-sql-statement-odbc.md)  
  
-   [建構資料指標的 SQL 陳述式](../../relational-databases/native-client-odbc-queries/constructing-sql-statements-for-cursors.md)  
  
-   [使用陳述式參數](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
-   [執行宣告&#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
-   [釋放陳述式控制代碼](../../relational-databases/native-client-odbc-queries/freeing-a-statement-handle.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
