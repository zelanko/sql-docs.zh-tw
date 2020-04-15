---
title: 處理結果 (ODBC) |微軟文件
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
ms.openlocfilehash: 39dafbb865ef951356bb01c4fd8f646bf943346b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304579"
---
# <a name="processing-results-odbc"></a>處理結果 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  應用程式提交 SQL 陳述式後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回產生的任何資料，做為一個或多個結果集。 結果集是一組符合查詢準則的資料列和資料行。 SELECT 陳述式、目錄函數以及某些預存程序會產生表格形式的結果集，供應用程式使用。 如果已執行的 SQL 陳述式是一個預存程序、包含多個命令的批次，或包含關鍵字的 SELECT 陳述式，則會有多個要處理的結果集。  
  
 ODBC 目錄函數也可以擷取資料。 例如[,SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)檢索有關數據源中列的數據。 這些結果集可以包含零或多個資料列。  
  
 GRANT 或 REVOKE 之類的 SQL 陳述式不會傳回結果集。 對於這些語句,來自**SQLExecute**或**SQLExecDirect**的返回代碼通常是該語句成功的唯一指示。  
  
 每個 INSERT、UPDATE 和 DELETE 陳述式都會傳回只包含受到修改影響之資料列數目的結果集。 當應用程式呼叫[SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)時,此計數可用。 ODBC 3.*x*應用程式必須調用**SQLRowCount**來檢索結果集,或者[SQLMore 結果](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)才能取消它。 當應用程式執行包含多個 INSERT、UPDATE 或 DELETE 語句的批處理或儲存過程時,必須使用**SQLRowCount**處理每個修改敘述的結果集,否則必須使用**SQLMoreResult**取消。 在批次或預存程序中加入 SET NOCOUNT ON 陳述式可以取消這些計數。  
  
 Transact-SQL 包括 SET NOCOUNT 陳述式。 啟用 NOCOUNT 選項時,SQL Server 不會返回受語句影響的行的計數 **,SQLRowCount**返回 0。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式版本引入了特定於驅動程式的[SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md)選項(SQL_SOPT_SS_NOCOUNT_STATUS),用於報告 NOCOUNT 選項是打開還是關閉。 每當**SQLRowCount**返回 0 時,應用程式都應測試SQL_SOPT_SS_NOCOUNT_STATUS。 如果返回**SQL_NC_ON,SQLRowCount**中的值 0 僅表示 SQL Server 未返回行計數。 如果返回SQL_NC_OFF,則表示 NOCOUNT 已關閉 **,SQLRowCount**中的值 0 表示該語句不會影響任何行。 當SQL_SOPT_SS_NOCOUNT_STATUSSQL_NC_OFF時,應用程式不應顯示**SQLRowCount**的值。 大型批次或預存程序可能包含多個 SET NOCOUNT 陳述式，因此，程式設計人員無法假設 SQL_SOPT_SS_NOCOUNT_STATUS 仍為常數。 每次**SQLRowCount**返回 0 時,都應測試該選項。  
  
 其他數個 Transact-SQL 陳述式會在訊息 (而非結果集) 中傳回其資料。 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式收到這些消息時,它將返回SQL_SUCCESS_WITH_INFO,讓應用程式知道資訊消息可用。 然後,應用程式可以調用**SQLGetDiagRec**來檢索這些消息。 使用此種方式運作的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式為：  
  
-   DBCC  
  
-   SET SHOWPLAN (適用於舊版的 SQL Server)  
  
-   SET STATISTICS  
  
-   PRINT  
  
-   RAISERROR  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 ODBC 驅動程式在嚴重性為 11 或更高的 RAISERROR 上返回SQL_ERROR。 如果 RAISERROR 的嚴重性為 19 以上，也會中斷連接。  
  
 若要從 SQL 陳述式處理結果集，應用程式會：  
  
-   決定結果集的特性。  
  
-   將資料行繫結到程式變數。  
  
-   擷取單一值、整個資料列的值，或多個資料列的值。  
  
-   測試是否有其他結果集，如果有，回到決定新結果集的特性。  
  
 從資料來源擷取資料列，然後將其傳回應用程式的過程稱為提取。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [確定結果集的特徵&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
-   [指派儲存體](../../relational-databases/native-client-odbc-results/assigning-storage.md)  
  
-   [提取結果資料](../../relational-databases/native-client-odbc-results/fetching-result-data.md)  
  
-   [映射資料類型&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/mapping-data-types-odbc.md)  
  
-   [資料類型使用方式](../../relational-databases/native-client-odbc-results/data-type-usage.md)  
  
-   [字元資料的自動轉譯](../../relational-databases/native-client-odbc-results/autotranslation-of-character-data.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL 伺服器本機用戶端&#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [處理結果「如何」主題&#40;ODBC&#41;](https://msdn.microsoft.com/library/772d9064-c91d-4cac-8b60-fcc16bf76e10)  
  
  
