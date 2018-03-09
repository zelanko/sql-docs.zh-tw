---
title: "記憶體 (ODBC) 中的所有值的資料表值參數的形式傳送資料 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), sending data to a stored procedure with all values in memory
ms.assetid: 8b96282f-00d5-4e28-8111-0a87ae6d7781
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b78fe6215d4d612b787cdd53316c66e30478fc34
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="sending-data-as-a-table-valued-parameter-with-all-values-in-memory-odbc"></a>使用記憶體中的所有值，將資料當做資料表值參數傳送 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主題描述所有的值都在記憶體中時，如何將資料當做資料表值參數傳送至預存程序。 如需示範資料表值參數的另一個範例，請參閱[使用資料表值參數 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md)。  
  
## <a name="prerequisite"></a>必要條件  
 此程序假設已在伺服器上執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)]：  
  
```  
create type TVParam as table(ProdCode integer, Qty integer)  
create procedure TVPOrderEntry(@CustCode varchar(5), @Items TVPParam,   
            @OrdNo integer output, @OrdDate datetime output)  
         as   
         set @OrdDate = GETDATE();  
         insert into TVPOrd (OrdDate, CustCode)   
values (@OrdDate, @CustCode) output OrdNo);   
         select @OrdNo = SCOPE_IDENTITY();   
         insert into TVPItem (OrdNo, ProdCode, Qty)  
select @OrdNo, @Items.ProdCode, @Items.Qty   
from @Items  
```  
  
## <a name="to-send-the-data"></a>傳送資料  
  
1.  宣告 SQL 參數的變數。 在此情況下，資料表值會完整保留在記憶體中，因此會將資料表值資料行的值宣告為陣列。  
  
    ```  
    SQLRETURN r;  
    // Variables for SQL parameters.  
    #define ITEM_ARRAY_SIZE 20  
  
    SQLCHAR CustCode[6];  
    SQLCHAR *TVP = (SQLCHAR *) "TVParam";  
    SQLINTEGER ProdCode[ITEM_ARRAY_SIZE], Qty[ITEM_ARRAY_SIZE];  
    SQLINTEGER OrdNo;  
    char OrdDate[23];  
  
    // Variables for indicator/length variables associated with parameters.  
    SQLLEN cbCustCode, cbTVP, cbProdCode[ITEM_ARRAY_SIZE], cbQty[ITEM_ARRAY_SIZE], cbOrdNo, cbOrdDate;  
    ```  
  
2.  繫結參數。 使用資料表值參數時，繫結參數是一個兩個階段的程序。 在第一個階段中，預存程序的 step 參數會以正常的方式繫結，如下所示。  
  
    ```  
    // Bind parameters for call to TVPOrderEntryDirect.  
    // 1 - Custcode input  
    r = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT,SQL_VARCHAR, SQL_C_CHAR, 5, 0, CustCode, sizeof(CustCode), &cbCustCode);  
  
    // 2 - Items TVP  
    r = SQLBindParameter(hstmt,   
        2,// ParameterNumber  
        SQL_PARAM_INPUT,// InputOutputType  
        SQL_C_DEFAULT,// ValueType   
        SQL_SS_TABLE,// Parametertype  
        ITEM_ARRAY_SIZE,// ColumnSize: For a table-valued parameter this is the row array size.  
        0,// DecimalDigits: For a table-valued parameter this is always 0.   
        TVP,// ParameterValuePtr: For a table-valued parameter this is the type name of the   
    //table-valued parameter, and also a token returned by SQLParamData.  
        SQL_NTS,// BufferLength: For a table-valued parameter this is the length of the type name or SQL_NTS.  
        &cbTVP);// StrLen_or_IndPtr: For a table-valued parameter this is the number of rows actually used.  
  
    // 3 - OrdNo output  
    r = SQLBindParameter(hstmt, 3, SQL_PARAM_OUTPUT,SQL_INTEGER, SQL_C_LONG, 0, 0, &OrdNo,  
       sizeof(SQLINTEGER), &cbOrdNo);  
    // 4 - OrdDate output  
    r = SQLBindParameter(hstmt, 4, SQL_PARAM_OUTPUT,SQL_TYPE_TIMESTAMP, SQL_C_CHAR, 23, 3, &OrdDate,   
       sizeof(OrdDate), &cbOrdDate);  
    ```  
  
3.  參數繫結的第二個階段是建立資料表值參數的資料行。 參數焦點會先設定為資料表值參數的序數。 然後會 SQLBindParameter 使用相同的方式，因為它們可以是參數的預存程序，但資料行序數 Sqlbindparameter 繫結資料表值的資料行。 如果有其他資料表值參數，則會輪流將焦點設定為每個資料表值參數，並繫結其資料行。 最後，參數焦點就會重設為 0。  
  
    ```  
    // Bind columns for the table-valued parameter (param 2).  
    // First set focus on param 2.  
    r = SQLSetStmtAttr(hstmt, SQL_SOPT_SS_PARAM_FOCUS, (SQLPOINTER) 2, SQL_IS_INTEGER);  
  
    // Col 1 - ProdCode  
    r = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT,SQL_INTEGER, SQL_C_LONG, 0, 0, ProdCode, sizeof(SQLINTEGER), cbProdCode);  
    // Col 2 - Qty  
    r = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT,SQL_INTEGER, SQL_C_LONG, 0, 0, Qty, sizeof(SQLINTEGER), cbQty);  
  
    // Reset param focus.  
    r = SQLSetStmtAttr(hstmt, SQL_SOPT_SS_PARAM_FOCUS, (SQLPOINTER) 0, SQL_IS_INTEGER);  
    ```  
  
4.  擴充參數緩衝區。 `cbTVP` 會設定為要傳送到伺服器的資料列數目。  
  
    ```  
    // Populate parameters.  
    cbTVP = 0; // Number of rows available for input.  
    strcpy_s((char *) CustCode, sizeof(CustCode), "CUST1"); cbCustCode = SQL_NTS;  
  
    ProdCode[cbTVP] = 1215;cbProdCode[cbTVP] = sizeof(SQLINTEGER);   
    Qty[cbTVP] = 5;cbQty[cbTVP] = sizeof(SQLINTEGER);   
    cbTVP++; // Number of rows available for input  
  
    ProdCode[cbTVP] = 1017;cbProdCode[cbTVP] = sizeof(SQLINTEGER);   
    Qty[cbTVP] = 2;cbQty[cbTVP] = sizeof(SQLINTEGER);   
    cbTVP++; // Number of rows available for input.  
    ```  
  
5.  呼叫程序：  
  
    ```  
    // Call the procedure.  
    r = SQLExecDirect(hstmt, (SQLCHAR *) "{call TVPOrderEntry(?, ?, ?, ?)}",SQL_NTS);  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 資料表值參數程式設計範例](http://msdn.microsoft.com/library/3f52b7a7-f2bd-4455-b79e-d015fb397726)  
  
  
