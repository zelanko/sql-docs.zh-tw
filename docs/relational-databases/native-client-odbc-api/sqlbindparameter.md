---
description: SQLBindParameter
title: SQLBindParameter |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aef702d89da9a4277fcc01bddc619eab5878ba6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428370"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  當用來提供原生用戶端 ODBC 驅動程式的資料時， **SQLBindParameter**可以消除資料轉換的負擔 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，進而大幅提升應用程式的用戶端和伺服器元件的效能。 其他優點包括插入或更新近似的數值資料類型時，降低有效位數的損失。  
  
> [!NOTE]  
>  將 **char** 和 **wchar** 類型的資料插入至影像資料行時，會使用傳入的資料大小，而不是轉換成二進位格式之後的資料大小。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式在任何參數陣列的單一陣列元素上碰到錯誤，驅動程式會繼續執行其餘陣列元素的陳述式。 如果應用程式已經繫結陳述式的參數狀態元素陣列，可以從陣列判斷產生錯誤的參數資料列。  
  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式，指定繫結輸入參數時的 SQL_PARAM_INPUT。 繫結使用 OUTPUT 關鍵字定義的預存程序參數時，只會指定 SQL_PARAM_OUTPUT 或 SQL_PARAM_INPUT_OUTPUT。  
  
 [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)如果系結 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 參數陣列的陣列元素在語句執行中造成錯誤，則 SQLRowCount 與 Native Client ODBC 驅動程式不可靠。 ODBC 陳述式屬性 SQL_ATTR_PARAMS_PROCESSED_PTR 會報告錯誤發生前處理的資料列數目。 接著，如果需要，此應用程式可以周遊其參數狀態陣列以探索成功執行的陳述式數目。  
  
## <a name="binding-parameters-for-sql-character-types"></a>SQL 字元類型的繫結參數  
 如果傳入的 SQL 資料類型是字元類型， *ColumnSize* 就會以字元為單位， (不是) 的位元組。 如果資料字串的長度（以位元組為單位）大於8000，則應該將 *ColumnSize* 設定為 **SQL_SS_LENGTH_UNLIMITED**，表示 SQL 類型的大小沒有任何限制。  
  
 比方說，如果 SQL 資料型別是 **SQL_WVARCHAR**， *ColumnSize* 就不能大於4000。 如果實際的資料長度大於4000，則應該將 *ColumnSize* 設定為 **SQL_SS_LENGTH_UNLIMITED** ，如此一來，驅動程式就會使用 **Nvarchar (max) ** 。  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter 和資料表值參數  
 如同其他參數類型，資料表值參數是由 SQLBindParameter 所系結。  
  
 繫結資料表值參數之後，也會一併繫結其資料行。 若要系結資料行，請呼叫 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) ，將 SQL_SOPT_SS_PARAM_FOCUS 設定為數據表值參數的序數。 然後，針對資料表值參數中的每個資料行呼叫 SQLBindParameter。 若要傳回到最上層參數繫結，將 SQL_SOPT_SS_PARAM_FOCUS 設定為 0。  
  
 如需有關將參數對應至資料表值參數之描述項欄位的詳細資訊，請參閱 [資料表值參數和資料行值的系結和資料傳輸](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 如需資料表值參數的詳細資訊，請參閱 [&#40;ODBC&#41;的資料表值參數 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>SQLBindParameter 對增強型日期和時間功能的支援  
 日期/時間類型的參數值會如 [從 C 轉換成 SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)所述進行轉換。 請注意，如果使用類型的對應結構 (**SQL_SS_TIME2_STRUCT**和**SQL_SS_TIMESTAMPOFFSET_STRUCT**) ，則類型**時間**和**datetimeoffset**的參數必須將*ValueType*指定為**SQL_C_DEFAULT**或**SQL_C_BINARY** 。  
  
 如需詳細資訊，請參閱 [&#40;ODBC&#41;的日期和時間改進 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLBindParameter 支援  
 **SQLBindParameter** 支援)  (udt 的大型 CLR 使用者自訂類型。 如需詳細資訊，請參閱 [&#40;ODBC&#41;的大型 CLR 使用者自訂類型 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 的執行詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLBindParameter 函式](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
