---
description: SQLGetDescField
title: SQLGetDescField |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetDescField function
ms.assetid: 3e59a37a-28ee-4c91-8968-7fe3b966739d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e81ed53721914502d1a4c90aeff9c55808588c7f
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810534"
---
# <a name="sqlgetdescfield"></a>SQLGetDescField
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 ODBC 驅動程式只會 (IRD) ，公開適用于實資料列描述項的驅動程式專屬描述項欄位。 在 IRD 內， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會透過驅動程式特定的資料行屬性來參考描述項欄位。 如需可用驅動程式特定描述項欄位完整清單的詳細資訊，請參閱 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)。  
  
 包含資料行識別項字串的描述項欄位常是零長度的字串。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的描述項欄位值都是唯讀的。  
  
 就像使用 SQLColAttribute 抓取的屬性一樣，也會針對結果集中的所有資料行報告資料列層級屬性 (（例如 SQL_CA_SS_COMPUTE_ID) ）的描述項欄位。  
  
## <a name="sqlgetdescfield-and-table-valued-parameters"></a>SQLGetDescField 和資料表值參數  
 SQLGetDescField 可以用來取得資料表值參數和資料表值參數資料行的擴充屬性值。 如需資料表值參數的詳細資訊，請參閱 [&#40;ODBC&#41;的資料表值參數 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlgetdescfield-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLGetDescField 支援  
 如需新日期/時間類型可用之描述項欄位的詳細資訊，請參閱 [參數和結果中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)。  
  
 如需詳細資訊，請參閱 [&#40;ODBC&#41;的日期和時間改進 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
 從開始 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ，如果您**的**應用程式使用 ODBC 3.8，SQLGetDescField 可以傳回**時間**類型**SQL_C_SS_TIME2** () 或**SQL_C_SS_TIMESTAMPOFFSET** (（而不是 **) **）。  
  
## <a name="sqlgetdescfield-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLGetDescField 支援  
 **SQLGetDescField** 支援)  (udt 的大型 CLR 使用者自訂類型。 如需詳細資訊，請參閱 [&#40;ODBC&#41;的大型 CLR 使用者自訂類型 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlgetdescfield-support-for-sparse-columns"></a>疏鬆資料行的 SQLGetDescField 支援  
 SQLGetDescField 可以用來查詢新的 IRD 欄位 SQL_CA_SS_IS_COLUMN_SET，以判斷資料行是否為 **column_set** 的資料行。  
  
 如需詳細資訊，請參閱 [&#40;ODBC&#41;的稀疏資料行支援 ](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。  
  
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
 [SQLGetDescField 函式](../../odbc/reference/syntax/sqlgetdescfield-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
