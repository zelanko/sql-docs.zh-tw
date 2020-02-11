---
title: SQLGetDescField |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetDescField function
ms.assetid: 3e59a37a-28ee-4c91-8968-7fe3b966739d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a92b3a9491b8424fb9015fc4d30875fedb38758
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62657777"
---
# <a name="sqlgetdescfield"></a>SQLGetDescField
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式只會針對「執行資料列描述元」（IRD）公開驅動程式特定的描述項欄位。 在 IRD 內， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會透過驅動程式特有的資料行屬性來參考描述項欄位。 如需可用驅動程式專屬描述項欄位的完整清單的詳細資訊，請參閱[SQLColAttribute](sqlcolattribute.md)。  
  
 包含資料行識別項字串的描述項欄位常是零長度的字串。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的描述項欄位值都是唯讀的。  
  
 就像使用 SQLColAttribute 抓取的屬性一樣，會針對結果集中的所有資料行，報告資料列層級屬性（例如 SQL_CA_SS_COMPUTE_ID）的描述項欄位。  
  
## <a name="sqlgetdescfield-and-table-valued-parameters"></a>SQLGetDescField 和資料表值參數  
 SQLGetDescField 可以用來取得資料表值參數和資料表值參數資料行之擴充屬性的值。 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlgetdescfield-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLGetDescField 支援  
 如需新日期/時間類型可用之描述項欄位的詳細資訊，請參閱[參數和結果中繼資料](../native-client-odbc-date-time/metadata-parameter-and-result.md)。  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
 從開始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，如果您的`SQL_C_SS_TIME2` `SQL_C_BINARY`應用程式`time`使用 ODBC 3.8，SQLGetDescField 可以傳回（適用于類型）或`SQL_C_SS_TIMESTAMPOFFSET` （適用于`datetimeoffset`）而不是。  
  
## <a name="sqlgetdescfield-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLGetDescField 支援  
 
  `SQLGetDescField` 支援大型 CLR 使用者定義型別 (UDT)。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlgetdescfield-support-for-sparse-columns"></a>疏鬆資料行的 SQLGetDescField 支援  
 SQLGetDescField 可以用來查詢新的 IRD 欄位 SQL_CA_SS_IS_COLUMN_SET 來判斷資料行是否為`column_set`資料行。  
  
 如需詳細資訊，請參閱[&#40;ODBC&#41;的稀疏資料行支援](../native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="example"></a>範例  
  
```  
typedef struct tagCOMPUTEBYLIST  
    {  
    SQLSMALLINT nBys;  
    SQLSMALLINT aByList[1];  
    } COMPUTEBYLIST;  
typedef COMPUTEBYLIST* PCOMPUTEBYLIST;   
  
SQLHDESC    hIRD;   
SQLINTEGER  cbIRD;   
SQLINTEGER  nSet = 0;   
  
// . . .  
// Execute a statement that contains a COMPUTE clause,  
//  then get the descriptor handle of the IRD and  
//  get some IRD values.  
  
SQLGetStmtAttr(g_hStmt, SQL_ATTR_IMP_ROW_DESC,  
    (SQLPOINTER) &hIRD, sizeof(SQLHDESC), &cbIRD);  
  
// For statement-wide column attributes, any  
//  descriptor record will do. You know that 1 exists,  
//  so use it.  
SQLGetDescField(hIRD, 1, SQL_CA_SS_NUM_COMPUTES,  
    (SQLPOINTER) &nComputes, SQL_IS_INTEGER, &cbIRD);  
  
if (nSet == 0)  
    {  
    SQLINTEGER      nOrderID;  
  
    printf_s("Normal result set.\n");  
  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        SQLGetDescField(hIRD, nCol+1,  
            SQL_CA_SS_COLUMN_ORDER,  
            (SQLPOINTER) &nOrderID, SQL_IS_INTEGER,  
            &cbIRD);  
  
        if (nOrderID != 0)  
            {  
            printf_s("Col in ORDER BY, pos: %ld",  
                nOrderID);  
            }  
            printf_s("\n");  
        }  
  
    printf_s("\n");  
    }  
else  
    {  
    PCOMPUTEBYLIST  pByList;  
    SQLSMALLINT     nBy;  
    SQLINTEGER      nColID;  
  
    printf_s("Computed result set number: %lu\n",  
        nSet);  
  
    SQLGetDescField(hIRD, 1, SQL_CA_SS_COMPUTE_BYLIST,  
        (SQLPOINTER) &pByList, SQL_IS_INTEGER,  
        &cbIRD);  
  
    if (pByList != NULL)  
        {  
        printf_s("Clause ordered by columns: ");  
        for (nBy = 0; nBy < pByList->nBys; )  
            {  
            printf_s("%u", pByList->aByList[nBy]);  
            nBy++;  
  
            if (nBy == pByList->nBys)  
                {  
                printf_s("\n");  
                }  
            else  
                {  
                printf_s(", ");  
                }  
            }  
        }  
    else  
        {  
        printf_s("Compute clause set not ordered.\n");  
        }  
  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        SQLGetDescField(hIRD, nCol+1,  
            SQL_CA_SS_COLUMN_ID, (SQLPOINTER) &nColID,  
            SQL_IS_INTEGER, &cbIRD);  
        printf_s("ColumnID: %lu, nColID);  
        }  
    printf_s("\n");  
    }  
  
if (SQLMoreResults(g_hStmt) == SQL_SUCCESS)  
    {  
    // Determine the result set indicator.  
    SQLGetDescField(hIRD, 1, SQL_CA_SS_COMPUTE_ID,  
        (SQLPOINTER) &nSet, SQL_IS_INTEGER, &cbIRD);  
    }  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetDescField 函式](https://go.microsoft.com/fwlink/?LinkId=59351)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
