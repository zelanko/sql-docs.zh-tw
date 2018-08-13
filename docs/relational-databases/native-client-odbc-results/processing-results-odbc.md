---
title: 處理結果 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], about result sets
- SQLRowCount function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- COMPUTE clause
- result sets [ODBC]
- COMPUTE BY clause
ms.assetid: 61a8db19-6571-47dd-84e8-fcc97cb60b45
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 78af5b7282ad0975f7588ae156acb73509cf7ae2
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39538728"
---
# <a name="processing-results-odbc"></a>處理結果 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  應用程式提交 SQL 陳述式後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回產生的任何資料，做為一個或多個結果集。 結果集是一組符合查詢準則的資料列和資料行。 SELECT 陳述式、目錄函數以及某些預存程序會產生表格形式的結果集，供應用程式使用。 如果已執行的 SQL 陳述式是一個預存程序、包含多個命令的批次，或包含關鍵字的 SELECT 陳述式，則會有多個要處理的結果集。  
  
 ODBC 目錄函數也可以擷取資料。 例如， [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)擷取有關資料來源中的資料行的資料。 這些結果集可以包含零或多個資料列。  
  
 GRANT 或 REVOKE 之類的 SQL 陳述式不會傳回結果集。 這些陳述式的傳回碼**SQLExecute**或是**SQLExecDirect**通常是成功的陳述式的唯一徵兆。  
  
 每個 INSERT、UPDATE 和 DELETE 陳述式都會傳回只包含受到修改影響之資料列數目的結果集。 這個計數會提供應用程式時呼叫[SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)。 ODBC 3。*x*應用程式必須呼叫**SQLRowCount**來擷取結果集或[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)將其取消即可。 當應用程式執行的批次或預存程序包含多個 INSERT、 UPDATE 或 DELETE 陳述式時，必須使用處理來自每個修改陳述式的結果集**SQLRowCount**或取消使用**SQLMoreResults**。 在批次或預存程序中加入 SET NOCOUNT ON 陳述式可以取消這些計數。  
  
 Transact-SQL 包括 SET NOCOUNT 陳述式。 當 NOCOUNT 選項設定上時，SQL Server 不會傳回受到陳述式的資料列計數並**SQLRowCount**會傳回 0。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式版本導入一個驅動程式專屬[SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md)選項 SQL_SOPT_SS_NOCOUNT_STATUS，來回報 NOCOUNT 選項開啟或關閉。 任何時候**SQLRowCount**傳回 0 時，應用程式應該測試 SQL_SOPT_SS_NOCOUNT_STATUS。 如果傳回 sql_nc_on，值為 0 時**SQLRowCount**只表示 SQL Server 尚未傳回資料列計數。 如果傳回 SQL_NC_OFF，表示 NOCOUNT 是關閉和值為 0 時**SQLRowCount**指出陳述式並未影響任何資料列。 應用程式應該不會顯示的值**SQLRowCount**當 SQL_SOPT_SS_NOCOUNT_STATUS 為 sql_nc_off 時。 大型批次或預存程序可能包含多個 SET NOCOUNT 陳述式，因此，程式設計人員無法假設 SQL_SOPT_SS_NOCOUNT_STATUS 仍為常數。 選擇應該測試每次**SQLRowCount**會傳回 0。  
  
 其他數個 Transact-SQL 陳述式會在訊息 (而非結果集) 中傳回其資料。 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式收到這些訊息，它會傳回 SQL_SUCCESS_WITH_INFO，讓應用程式知道有參考用訊息。 應用程式接著可以呼叫**SQLGetDiagRec**來擷取這些訊息。 使用此種方式運作的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式為：  
  
-   DBCC  
  
-   SET SHOWPLAN (適用於舊版的 SQL Server)  
  
-   SET STATISTICS  
  
-   PRINT  
  
-   RAISERROR  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會針對嚴重性為 11 以上的 RAISERROR 傳回 SQL_ERROR。 如果 RAISERROR 的嚴重性為 19 以上，也會中斷連接。  
  
 若要從 SQL 陳述式處理結果集，應用程式會：  
  
-   決定結果集的特性。  
  
-   將資料行繫結到程式變數。  
  
-   擷取單一值、整個資料列的值，或多個資料列的值。  
  
-   測試是否有其他結果集，如果有，回到決定新結果集的特性。  
  
 從資料來源擷取資料列，然後將其傳回應用程式的過程稱為提取。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [決定結果集的特性&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
-   [指派儲存體](../../relational-databases/native-client-odbc-results/assigning-storage.md)  
  
-   [提取結果資料](../../relational-databases/native-client-odbc-results/fetching-result-data.md)  
  
-   [對應資料類型&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/mapping-data-types-odbc.md)  
  
-   [資料類型使用方式](../../relational-databases/native-client-odbc-results/data-type-usage.md)  
  
-   [字元資料的自動轉譯](../../relational-databases/native-client-odbc-results/autotranslation-of-character-data.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [處理結果使用說明主題&#40;ODBC&#41;](http://msdn.microsoft.com/library/772d9064-c91d-4cac-8b60-fcc16bf76e10)  
  
  
