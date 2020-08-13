---
title: 使用資料分類搭配 Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-makouz
ms.author: v-makouz
manager: kenvh
ms.openlocfilehash: 63600f98fcf86fb9549c6da91224988ce7483eee
ms.sourcegitcommit: 41ff0446bd8e4380aad40510ad579a3a4e096dfa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2020
ms.locfileid: "86465315"
---
# <a name="data-classification"></a>資料分類
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>概觀
基於管理敏感性資料的目的，SQL Server 和 Azure SQL Server 引進了提供具有敏感性中繼資料之資料庫資料行的功能，讓用戶端應用程式能夠根據資料保護原則來處理不同類型的敏感性資料 (例如，健康情況、財務等)。

如需如何將分類指派給資料行的詳細資訊，請參閱 [SQL 資料探索與分類](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification?view=sql-server-2017)。

Microsoft ODBC Driver 17.2 允許使用 SQL_CA_SS_DATA_CLASSIFICATION 欄位識別碼，透過 SQLGetDescField 來擷取此中繼資料。

## <a name="format"></a>[格式]
SQLGetDescField 具有下列語法：

```  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```
*DescriptorHandle*  
 [輸入] IRD (實作資料列描述項) 控制代碼。 可以透過 SQL_ATTR_IMP_ROW_DESC 陳述式屬性呼叫 SQLGetStmtAttr 來擷取
  
 *RecNumber*  
 [輸入] 0
  
 *FieldIdentifier*  
 [輸入] SQL_CA_SS_DATA_CLASSIFICATION
  
 *ValuePtr*  
 [輸出] 輸出緩衝區
  
 *BufferLength*  
 [輸入] 輸出緩衝區的長度 (以位元組為單位)

 *StringLengthPtr* [輸出] 緩衝區的指標，此緩衝區會傳回可在 *ValuePtr* 中傳回的位元組總數。
 
> [!NOTE]
> 如果緩衝區的大小是未知的，則可搭配 NULL 的 *ValuePtr* 來呼叫 SQLGetDescField，並檢查 *StringLengthPtr* 的值來進行判斷。
 
如果無法取得資料分類資訊，將會傳回「描述項欄位無效」  錯誤。

成功呼叫 SQLGetDescField 之後，透過 *Valueptr* 指向其中的緩衝區將包含下列資料：

 `nn nn [n sensitivitylabels] tt tt [t informationtypes] cc cc [c columnsensitivitys]`

> [!NOTE]
> `nn nn`、`tt tt` 和 `cc cc` 是多位元組整數，其會以最小顯著性位元組儲存於最低位址。

*`sensitivitylabel`* 和 *`informationtype`* 的形式如下

 `nn [n bytes name] ii [i bytes id]`

*`columnsensitivity`* 的形式如下

 `nn nn [n sensitivityprops]`

針對每個資料行 *(c)* ，均存在 *n* 個 4 位元組的 *`sensitivityprops`* ：

 `ss ss tt tt`

s：在 *`sensitivitylabels`* 陣列中編製索引，如果未加上標籤，則為 `FF FF`

t：在 *`informationtypes`* 陣列中編製索引，如果未加上標籤，則為 `FF FF`


<br><br>
資料的格式可以利用下列虛擬結構來表示：

```
struct IDnamePair {
 BYTE nameLen;
 USHORT name[nameLen];
 BYTE idLen;
 USHORT id[idLen];
};

struct SensitivityProp {
 USHORT labelIdx;
 USHORT infoTypeIdx;
};

USHORT nLabels;
struct IDnamePair labels[nLabels];
USHORT nInfoTypes;
struct IDnamePair infotypes[nInfoTypes];
USHORT nColumns;
struct {
 USHORT nProps;
 struct SensitivityProp[nProps];
} columnClassification[nColumns];
```


## <a name="code-sample"></a>程式碼範例
示範如何讀取資料分類中繼資料的測試應用程式。 在 Windows 上，可以使用 `cl /MD dataclassification.c /I (directory of msodbcsql.h) /link odbc32.lib` 進行編譯，並以連接字串和 SQL 查詢 (傳回已分類的資料行) 作為參數來執行：

```
#ifdef _WIN32
#include <windows.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include <msodbcsql.h>
#include <stdio.h>
SQLHANDLE env, dbc, stmt;
void checkRC_exit(SQLRETURN rc, SQLHANDLE hand, SQLSMALLINT htype, int retcode, char *action)
{
    if ((rc == SQL_ERROR || rc == SQL_SUCCESS_WITH_INFO) && hand)
    {
        char msg[1024], state[6];
        int i = 0;
        SQLRETURN rc2;
        SQLINTEGER err;
        SQLSMALLINT lenout;
        while ((rc2 = SQLGetDiagRec(htype, hand, ++i, state, &err, msg, sizeof(msg), &lenout)) == SQL_SUCCESS ||
            rc2 == SQL_SUCCESS_WITH_INFO)
            printf("%d (%d)[%s]%s\n", i, err, state, msg);
    }
    if (rc == SQL_ERROR && retcode)
    {
        printf("Error occurred%s%s\n", action ? " upon " : "", action ? action : "");
        exit(retcode);
    }
}
void printLabelInfo(char *type, char **pptr)
{
    char *ptr = *pptr;
    unsigned short nlabels;
    printf("----- %s(%u) -----\n", type, nlabels = *(unsigned short*)ptr);
    ptr += sizeof(unsigned short);
    while (nlabels--)
    {
        int namelen, idlen;
        char *nameptr, *idptr;
        namelen = *ptr++;
        nameptr = ptr;
        ptr += namelen * 2;
        idlen = *ptr++;
        idptr = ptr;
        ptr += idlen * 2;
        wprintf(L"Name: \"%.*s\" Id: \"%.*s\"\n", namelen, nameptr, idlen, idptr);
    }
    *pptr = ptr;
}
int main(int argc, char **argv)
{
    unsigned char *dcbuf;
    unsigned int dclen = 0;
    SQLRETURN rc;
    SQLHANDLE ird;
    if (argc < 3)
    {
        fprintf(stderr, "usage: dataclassification connstr query\n");
        return 1;
    }
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_ENV, 0, &env), 0, 0,
        2, "allocate environment");
    checkRC_exit(SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0), env, SQL_HANDLE_ENV,
        3, "set ODBC version");
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc), env, SQL_HANDLE_ENV,
        4, "allocate connection");
    checkRC_exit(SQLDriverConnect(dbc, 0, argv[1], SQL_NTS, 0, 0, 0, SQL_DRIVER_NOPROMPT), dbc, SQL_HANDLE_DBC,
        5, "connect to server");
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt), dbc, SQL_HANDLE_DBC,
        6, "allocate statement");
    checkRC_exit(SQLExecDirect(stmt, argv[2], SQL_NTS), stmt, SQL_HANDLE_STMT,
        7, "execute query");
    checkRC_exit(SQLGetStmtAttr(stmt, SQL_ATTR_IMP_ROW_DESC, (SQLPOINTER)&ird, SQL_IS_POINTER, 0), stmt, SQL_HANDLE_STMT,
        8, "get IRD handle");
    rc = SQLGetDescFieldW(ird, 0, SQL_CA_SS_DATA_CLASSIFICATION, dcbuf, 0, &dclen);
    if (rc != SQL_SUCCESS && rc != SQL_SUCCESS_WITH_INFO)
    {
        checkRC_exit(rc, ird, SQL_HANDLE_DESC, 0, 0);
        printf("Error reading SQL_CA_SS_DATA_CLASSIFICATION IRD field. Ensure that the driver and\n"
            "server both support the Data Classification feature, and that the query returns columns\n"
            "with classification information.\n");
    }
    else
    {
        SQLINTEGER dclenout;
        unsigned char *dcptr;
        unsigned short ncols;
        printf("Data Classification information (%u bytes):\n", dclen);
        if (!(dcbuf = malloc(dclen)))
        {
            printf("Memory Allocation Error");
            return 9;
        }
        checkRC_exit(SQLGetDescFieldW(ird, 0, SQL_CA_SS_DATA_CLASSIFICATION, dcbuf, dclen, &dclenout),
            ird, SQL_HANDLE_DESC, 10, "reading SQL_CA_SS_DATA_CLASSIFICATION");
        dcptr = dcbuf;
        printLabelInfo("Labels", &dcptr);
        printLabelInfo("Information Types", &dcptr);
        printf("----- Column Sensitivities(%u) -----\n", ncols = *(unsigned short*)dcptr);
        dcptr += sizeof(unsigned short);
        while (ncols--)
        {
            unsigned short nprops = *(unsigned short*)dcptr;
            dcptr += sizeof(unsigned short);
            while (nprops--)
            {
                unsigned short labelidx, typeidx;
                labelidx = *(unsigned short*)dcptr; dcptr += sizeof(unsigned short);
                typeidx = *(unsigned short*)dcptr; dcptr += sizeof(unsigned short);
                printf(labelidx == 0xFFFF ? "(none) " : "%u ", labelidx);
                printf(typeidx == 0xFFFF ? "(none)\n" : "%u\n", typeidx);
            }
            printf("-----\n");
        }
        if (dcptr != dcbuf + dclen)
        {
            printf("Error: unexpected parse of DATACLASSIFICATION data\n");
            return 11;
        }
        free(dcbuf);
    }
    return 0;
}
```

## <a name="supported-version"></a><a name="bkmk-version"></a>支援的版本
若將 `FieldIdentifier` 設定為 `SQL_CA_SS_DATA_CLASSIFICATION` (1237)，Microsoft ODBC Driver 17.2 即允許透過 `SQLGetDescField` 擷取資料分類資訊。 

從 Microsoft ODBC Driver 17.4.1.1 開始，您可以使用 `SQL_CA_SS_DATA_CLASSIFICATION_VERSION` (1238) 欄位識別碼，透過 `SQLGetDescField` 來擷取伺服器所支援的資料分類版本。 在 17.4.1.1 中，會將支援的資料分類版本設定為 "2"。

 

從 17.4.2.1 開始導入了預設版本的資料分類，並將其設定為 "1"，而且版本驅動程式正在向 SQL Server 報告支援此版本。 新的連線屬性 `SQL_COPT_SS_DATACLASSIFICATION_VERSION` (1400) 可讓應用程式將支援的資料分類版本從 "1" 變更為支援的最大值。  

範例： 

若要設定版本，應該在 SQLConnect 或 SQLDriverConnect 呼叫之前進行此呼叫：
```
ret = SQLSetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)2, SQL_IS_INTEGER);
```

目前支援的資料分類版本值可透過 SQLGetConnectAttr 呼叫來擷取： 
```
ret = SQLGetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)&dataClassVersion, SQL_IS_INTEGER, 0);
```

