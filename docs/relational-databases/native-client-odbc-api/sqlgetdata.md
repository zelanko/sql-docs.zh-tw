---
title: SQLGetData | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLGetData function
ms.assetid: 204848be-8787-45b4-816f-a60ac9d56fcf
caps.latest.revision: "42"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e738c8b3f4c2200287a7c4dc9578951e90c8dd8
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="sqlgetdata"></a>SQLGetData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLGetData**用來擷取結果集資料，而不繫結資料行值。 **SQLGetData**相同的資料行的資料行中擷取大量的資料可以連續呼叫**文字**， **ntext**，或**映像**資料類型.  
  
 不會要求應用程式繫結變數來擷取結果集資料。 任何資料行的資料可以從擷取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式使用**SQLGetData**。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不支援使用**SQLGetData**來依隨機資料行順序擷取資料。 使用未繫結的所有資料行處理**SQLGetData**必須具有較高的資料行序數以上的繫結的資料行結果集內。 應用程式必須處理從最低未繫結序數資料行值到最高值的資料。 嘗試從編號序數較低的資料行擷取資料將會產生錯誤。 如果應用程式使用伺服器資料指標來報告結果集資料列，則應用程式可以提取目前的資料列，然後再提取資料行的值。 如果預設的唯讀、 順向資料指標上執行的陳述式，則您必須重新執行陳述式，備份**SQLGetData**。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會精確地報告的長度**文字**， **ntext**，和**映像**使用擷取資料**SQLGetData**. 應用程式可以善用*StrLen_or_IndPtr*參數傳回快速擷取 long 資料。  
  
> [!NOTE]  
>  對於大數值類型*StrLen_or_IndPtr*會在資料截斷的情況下傳回 SQL_NO_TOTAL。  
  
## <a name="sqlgetdata-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLGetData 支援  
 結果資料行值的日期/時間類型轉換中所述[從 SQL 轉換成 C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)。  
  
 如需詳細資訊，請參閱[日期和時間增強功能 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlgetdata-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLGetData 支援  
 **SQLGetData**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱[Large CLR User-Defined 類型 &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="example"></a>範例  
  
```  
SQLHDBC     hDbc = NULL;  
SQLHSTMT    hStmt = NULL;  
long        lEmpID;  
PBYTE       pPicture;  
SQLINTEGER  pIndicators[2];  
  
// Get an environment, connection, and so on.  
...  
  
// Get a statement handle and execute a command.  
SQLAllocHandle(SQL_HANDLE_STMT, hDbc, &hStmt);  
  
if (SQLExecDirect(hStmt,  
    (SQLCHAR*) "SELECT EmployeeID, Photo FROM Employees",  
    SQL_NTS) == SQL_ERROR)  
    {  
    // Handle error and return.  
    }  
  
// Retrieve data from row set.  
SQLBindCol(hStmt, 1, SQL_C_LONG, (SQLPOINTER) &lEmpID, sizeof(long),  
    &pIndicators[0]);  
  
while (SQLFetch(hStmt) == SQL_SUCCESS)  
    {  
    cout << "EmployeeID: " << lEmpID << "\n";  
  
    // Call SQLGetData to determine the amount of data that's waiting.  
    if (SQLGetData(hStmt, 2, SQL_C_BINARY, pPicture, 0, &pIndicators[1])  
        == SQL_SUCCESS_WITH_INFO)  
        {  
        cout << "Photo size: " pIndicators[1] << "\n\n";  
  
        // Get all the data at once.  
        pPicture = new BYTE[pIndicators[1]];  
        if (SQLGetData(hStmt, 2, SQL_C_DEFAULT, pPicture,  
            pIndicators[1], &pIndicators[1]) != SQL_SUCCESS)  
            {  
            // Handle error and continue.  
            }  
  
        delete [] pPicture;  
        }  
    else  
        {  
        // Handle error on attempt to get data length.  
        }  
    }  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetData 函數](http://go.microsoft.com/fwlink/?LinkId=59350)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
