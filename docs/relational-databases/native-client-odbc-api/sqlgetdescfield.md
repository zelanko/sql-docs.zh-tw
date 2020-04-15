---
title: SQLGetDescField |微軟文件
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
ms.openlocfilehash: 341a9fe5c5919093853b0c62c7148515380a0551
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299570"
---
# <a name="sqlgetdescfield"></a>SQLGetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 ODBC 驅動程式僅公開實現行描述符 (IRD) 的特定於驅動程式的描述符位。 在 IRD[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中,描述符欄位透過特定於驅動程式的列屬性引用。 有關可用特定於驅動程式的描述符位的完整清單的資訊,請參閱[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)。  
  
 包含資料行識別項字串的描述項欄位常是零長度的字串。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的描述項欄位值都是唯讀的。  
  
 與使用 SQLColAttribute 檢索的屬性一樣,報告行級屬性(如SQL_CA_SS_COMPUTE_ID)的描述符欄位將報告結果集中的所有列。  
  
## <a name="sqlgetdescfield-and-table-valued-parameters"></a>SQLGetDescField 和資料表值參數  
 SQLGetDescField 可用於獲取表值參數和表值參數列的擴展屬性的值。 有關表值參數的詳細資訊,請參閱[&#40;ODBC&#41;的表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlgetdescfield-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLGetDescField 支援  
 關於新日期/時間類型可用的描述符位的資訊,請參閱[參數和結果中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)。  
  
 有關詳細資訊,請參閱[&#40;ODBC&#41;的日期和時間改進](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
 從[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始,如果您的應用程式使用 ODBC 3.8,SQLGetDescField 可以返回**SQL_C_SS_TIME2(** 對於**時間**類型)或**SQL_C_SS_TIMESTAMPOFFSET(** 對於**日期時間偏移**),而不是**SQL_C_BINARY。**  
  
## <a name="sqlgetdescfield-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLGetDescField 支援  
 **SQLGetDescField**支援大型 CLR 用戶定義類型 (UDT)。 有關詳細資訊,請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlgetdescfield-support-for-sparse-columns"></a>疏鬆資料行的 SQLGetDescField 支援  
 SQLGetDescField 可用於查詢新的 IRD 欄位SQL_CA_SS_IS_COLUMN_SET以確定列是否為**column_set**列。  
  
 有關詳細資訊,請參閱[稀疏列支援&#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。  
  
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
 [SQLGetDescfield 函數](https://go.microsoft.com/fwlink/?LinkId=59351)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
