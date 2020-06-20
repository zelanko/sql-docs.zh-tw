---
title: SQLGetData |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetData function
ms.assetid: 204848be-8787-45b4-816f-a60ac9d56fcf
author: rothja
ms.author: jroth
ms.openlocfilehash: 1d8633a66b9c6d1896f95275380d73ab69cb873d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022258"
---
# <a name="sqlgetdata"></a>SQLGetData
  **SQLGetData**是用來在不系結資料行值的情況下，抓取結果集資料。 可以在相同資料行上連續呼叫**SQLGetData** ，以從具有**text**、 **Ntext**或**image**資料類型的資料行中取出大量資料。  
  
 不會要求應用程式繫結變數來擷取結果集資料。 您可以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用**SQLGetData**，從 Native Client ODBC 驅動程式中取出任何資料行的資料。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式不支援使用**SQLGetData**以隨機的資料行順序來取得資料。 所有使用**SQLGetData**處理的未系結資料行，都必須具有比結果集中系結資料行更高的資料行序數。 應用程式必須處理從最低未繫結序數資料行值到最高值的資料。 嘗試從編號序數較低的資料行擷取資料將會產生錯誤。 如果應用程式使用伺服器資料指標來報告結果集資料列，則應用程式可以提取目前的資料列，然後再提取資料行的值。 如果語句是在預設的唯讀、順向資料指標上執行，您必須重新執行語句來備份**SQLGetData**。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會使用**SQLGetData**，正確地報告**text**、 **Ntext**和**image**資料的長度。 應用程式可以充分利用*StrLen_or_IndPtr*參數 return 來快速取出長資料。  
  
> [!NOTE]  
>  對於大數數值型別， *StrLen_or_IndPtr*將會在資料截斷的情況下傳回 SQL_NO_TOTAL。  
  
## <a name="sqlgetdata-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLGetData 支援  
 日期/時間類型的結果資料行值會轉換，如[從 SQL 轉換為 C](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)中所述。  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlgetdata-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLGetData 支援  
 **SQLGetData**支援大型 CLR 使用者定義型別（udt）。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
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
 [SQLGetData 函式](https://go.microsoft.com/fwlink/?LinkId=59350)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
