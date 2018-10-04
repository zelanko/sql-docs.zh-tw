---
title: 執行查詢 (ODBC) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 476ec6fc6ea5a41db63318feda7e06eea2e5c191
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628496"
---
# <a name="executing-queries-odbc"></a>執行查詢 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  當 ODBC 應用程式將連接控制代碼初始化並連接資料來源後，會在連接控制代碼上配置一個或多個陳述式控制代碼。 接著可執行應用程式[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]陳述式控制代碼上的陳述式。 執行 SQL 陳述式的一般事件序列是：  
  
1.  設定任何需要的陳述式屬性。  
  
2.  建構陳述式。  
  
3.  執行陳述式。  
  
4.  擷取任何結果集。  
  
 當應用程式擷取在 (由 SQL 陳述式傳回的) 所有結果集的資料列後，可以在相同陳述式控制代碼上執行另一個查詢。 如果應用程式會判斷它不需要擷取特定的結果集中的所有資料列，它可以取消結果集藉由呼叫的 rest [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)或是[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)。  
  
 在 ODBC 應用程式中，如果您必須用不同資料多次執行相同的 SQL 陳述式，則在 SQL 陳述式的建構中使用由問號 (?) 所代表的參數標記：  
  
```  
INSERT INTO MyTable VALUES (?, ?, ?)  
```  
  
 每個參數標記可以再繫結至程式變數藉由呼叫[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)。  
  
 在執行所有 SQL 陳述式，而且也處理其結果集之後，應用程式會釋放陳述式控制代碼。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援多個陳述式控制代碼，每個連接控制代碼。 由於交易是在連接層級管理，因此在所有陳述式控制代碼上所執行的所有工作，會在單一連接控制代碼上管理成為相同交易的一部分。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [配置陳述式控制代碼](../../relational-databases/native-client-odbc-queries/allocating-a-statement-handle.md)  
  
-   [建構 SQL 陳述式&#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/constructing-an-sql-statement-odbc.md)  
  
-   [建構資料指標的 SQL 陳述式](../../relational-databases/native-client-odbc-queries/constructing-sql-statements-for-cursors.md)  
  
-   [使用陳述式參數](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
-   [執行陳述式&#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
-   [釋放陳述式控制代碼](../../relational-databases/native-client-odbc-queries/freeing-a-statement-handle.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
