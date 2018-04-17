---
title: SQLGetDescField |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetDescField function
ms.assetid: 3e59a37a-28ee-4c91-8968-7fe3b966739d
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: adeebdd9a2541e1dd33b9cfb52775c56fd8cb109
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetdescfield"></a>SQLGetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會公開實作資料列描述項 (IRD) 只的驅動程式專屬描述項欄位。 在 IRD 內[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]描述項欄位會透過驅動程式特有的資料行屬性來參考。 可用的驅動程式專屬描述項欄位的完整清單的相關資訊，請參閱[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)。  
  
 包含資料行識別項字串的描述項欄位常是零長度的字串。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的描述項欄位值都是唯讀的。  
  
 類似的 SQLColAttribute、 擷取報表資料列層級屬性 （例侞 SQL_CA_SS_COMPUTE_ID) 會報告結果集中的所有資料行的描述項欄位的屬性。  
  
## <a name="sqlgetdescfield-and-table-valued-parameters"></a>SQLGetDescField 和資料表值參數  
 SQLGetDescField 可以用來取得資料表值參數和資料表值參數資料行的擴充屬性的值。 如需有關資料表值參數的詳細資訊，請參閱[資料表值參數 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlgetdescfield-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLGetDescField 支援  
 將新的日期/時間類型與可用的描述項欄位的相關資訊，請參閱[and Result Metadata<](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)。  
  
 如需詳細資訊，請參閱[日期和時間增強功能 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
 從開始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，SQLGetDescField 可以傳回**SQL_C_SS_TIME2** (如**時間**類型) 或**SQL_C_SS_TIMESTAMPOFFSET** (如**datetimeoffset**) 而不是**SQL_C_BINARY**，如果您的應用程式使用 ODBC 3.8 的話。  
  
## <a name="sqlgetdescfield-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLGetDescField 支援  
 **SQLGetDescField**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱[Large CLR User-Defined 類型 & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlgetdescfield-support-for-sparse-columns"></a>疏鬆資料行的 SQLGetDescField 支援  
 SQLGetDescField 可以用來查詢新增的 IRD field SQL_CA_SS_IS_COLUMN_SET，以判斷資料行是否為**column_set**資料行。  
  
 如需詳細資訊，請參閱[疏鬆資料行支援&#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。  
  
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
 [SQLGetDescField 函數](http://go.microsoft.com/fwlink/?LinkId=59351)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
