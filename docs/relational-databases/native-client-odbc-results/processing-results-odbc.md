---
title: 處理結果（ODBC） |Microsoft Docs
description: 瞭解如何處理 SQL Server 在 ODBC 應用程式提交 SQL 語句時傳回的資料。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6afb7460e4ceb09bff7b79e360fafcd8eb541703
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774250"
---
# <a name="processing-results-odbc"></a>處理結果 (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  應用程式提交 SQL 陳述式後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回產生的任何資料，做為一個或多個結果集。 結果集是一組符合查詢準則的資料列和資料行。 SELECT 陳述式、目錄函數以及某些預存程序會產生表格形式的結果集，供應用程式使用。 如果已執行的 SQL 陳述式是一個預存程序、包含多個命令的批次，或包含關鍵字的 SELECT 陳述式，則會有多個要處理的結果集。  
  
 ODBC 目錄函數也可以擷取資料。 例如， [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)會抓取資料來源中有關資料行的資料。 這些結果集可以包含零或多個資料列。  
  
 GRANT 或 REVOKE 之類的 SQL 陳述式不會傳回結果集。 針對這些語句， **SQLExecute**或**SQLExecDirect**的傳回碼通常是語句成功的唯一指示。  
  
 每個 INSERT、UPDATE 和 DELETE 陳述式都會傳回只包含受到修改影響之資料列數目的結果集。 當應用程式呼叫[SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)時，就可以使用此計數。 ODBC 3。*x*應用程式必須呼叫**SQLRowCount**來取得結果集或[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) ，才能將它取消。 當應用程式執行包含多個 INSERT、UPDATE 或 DELETE 子句的批次或預存程式時，必須使用**SQLRowCount**來處理每個修改語句的結果集，或使用**SQLMoreResults**來取消。 在批次或預存程序中加入 SET NOCOUNT ON 陳述式可以取消這些計數。  
  
 Transact-SQL 包括 SET NOCOUNT 陳述式。 當 NOCOUNT 選項設定為 on 時，SQL Server 不會傳回受語句影響的資料列計數，而**SQLRowCount**會傳回0。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式版本引進驅動程式特有的[SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md)選項 SQL_SOPT_SS_NOCOUNT_STATUS，以報告 NOCOUNT 選項為開啟或關閉。 每當**SQLRowCount**傳回0時，應用程式應該測試 SQL_SOPT_SS_NOCOUNT_STATUS。 如果傳回 SQL_NC_ON，則**SQLRowCount**中0的值只表示 SQL Server 未傳回資料列計數。 如果傳回 SQL_NC_OFF，則表示 NOCOUNT 是 OFF，而**SQLRowCount**的值則表示語句不會影響任何資料列。 當 SQL_SOPT_SS_NOCOUNT_STATUS SQL_NC_OFF 時，應用程式不應該顯示**SQLRowCount**的值。 大型批次或預存程序可能包含多個 SET NOCOUNT 陳述式，因此，程式設計人員無法假設 SQL_SOPT_SS_NOCOUNT_STATUS 仍為常數。 每次**SQLRowCount**傳回0時，應該測試此選項。  
  
 其他數個 Transact-SQL 陳述式會在訊息 (而非結果集) 中傳回其資料。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式收到這些訊息時，它會傳回 SQL_SUCCESS_WITH_INFO，讓應用程式知道有參考用訊息。 然後，應用程式可以呼叫**SQLGetDiagRec**來取得這些訊息。 使用此種方式運作的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式為：  
  
-   DBCC  
  
-   SET SHOWPLAN (適用於舊版的 SQL Server)  
  
-   SET STATISTICS  
  
-   PRINT  
  
-   RAISERROR  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會在嚴重性為11（含）以上的 RAISERROR 上傳回 SQL_ERROR。 如果 RAISERROR 的嚴重性為 19 以上，也會中斷連接。  
  
 若要從 SQL 陳述式處理結果集，應用程式會：  
  
-   決定結果集的特性。  
  
-   將資料行繫結到程式變數。  
  
-   擷取單一值、整個資料列的值，或多個資料列的值。  
  
-   測試是否有其他結果集，如果有，回到決定新結果集的特性。  
  
 從資料來源擷取資料列，然後將其傳回應用程式的過程稱為提取。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [判斷結果集的特性 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
-   [指派儲存體](../../relational-databases/native-client-odbc-results/assigning-storage.md)  
  
-   [提取結果資料](../../relational-databases/native-client-odbc-results/fetching-result-data.md)  
  
-   [&#40;ODBC&#41;對應資料類型](../../relational-databases/native-client-odbc-results/mapping-data-types-odbc.md)  
  
-   [資料類型使用方式](../../relational-databases/native-client-odbc-results/data-type-usage.md)  
  
-   [字元資料的自動轉譯](../../relational-databases/native-client-odbc-results/autotranslation-of-character-data.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [處理結果如何 &#40;ODBC&#41;的 how to 主題](https://msdn.microsoft.com/library/772d9064-c91d-4cac-8b60-fcc16bf76e10)  
  
  
