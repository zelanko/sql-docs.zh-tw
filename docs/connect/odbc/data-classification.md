---
title: 搭配 Microsoft ODBC Driver for SQL Server 使用資料分類 |Microsoft Docs
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
ms.openlocfilehash: 8f0f821890cabe25a9abb572e453c9846c75ec94
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041128"
---
# <a name="data-classification"></a>資料分類
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>概觀
基於管理敏感性資料的目的，SQL Server 和 Azure SQL Server 引進了提供具有敏感性中繼資料之資料庫資料行的功能，可讓用戶端應用程式處理不同類型的敏感性資料（例如健康情況、財務等等）。）（根據資料保護原則）。

如需如何將分類指派至資料行的詳細資訊，請參閱[SQL 資料探索和分類](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification?view=sql-server-2017)。

Microsoft ODBC Driver 17.2 允許使用 SQL_CA_SS_DATA_CLASSIFICATION 欄位識別碼，透過 SQLGetDescField 來抓取此中繼資料。

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
 源IRD （執行資料列描述項）控制碼。 可透過呼叫 SQLGetStmtAttr 與 SQL_ATTR_IMP_ROW_DESC 語句屬性來抓取
  
 *RecNumber*  
 [輸入] 0
  
 *FieldIdentifier*  
 [輸入] SQL_CA_SS_DATA_CLASSIFICATION
  
 *ValuePtr*  
 輸出輸出緩衝區
  
 *BufferLength*  
 源輸出緩衝區的長度（以位元組為單位）

 *StringLengthPtr* [Output] 要傳回*valueptr 是*中傳回之位元組總數的緩衝區指標。
 
> [!NOTE]
> 如果緩衝區的大小不明，可以藉由呼叫 SQLGetDescField 並將*valueptr 是*當做 Null，並檢查*StringLengthPtr*的值來判斷。
 
如果資料分類資訊無法使用，則會傳回*不正確描述項欄位*錯誤。

成功呼叫 SQLGetDescField 時， *valueptr 是*所指向的緩衝區會包含下列資料：

 `nn nn [n sensitivitylabels] tt tt [t informationtypes] cc cc [c columnsensitivitys]`

> [!NOTE]
> `nn nn`，`tt tt`，而 `cc cc` 是多位元組整數，以最低的位址儲存最小的位元組。

*`sensitivitylabel`* 和 *`informationtype`* 的格式都是

 `nn [n bytes name] ii [i bytes id]`

*`columnsensitivity`* 的格式為

 `nn nn [n sensitivityprops]`

針對每個資料行 *（c）* ，會有*n* 4 位元組 *`sensitivityprops`* ：

 `ss ss tt tt`

s-索引至 *`sensitivitylabels`* 陣列中，`FF FF` （如果未加上標籤）

t-索引至 *`informationtypes`* 陣列中，`FF FF` （如果未加上標籤）


<br><br>
資料的格式可以表示為下列虛擬結構：

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
示範如何讀取資料分類中繼資料的測試應用程式。 在 Windows 上，可以使用 `cl /MD dataclassification.c /I (directory of msodbcsql.h) /link odbc32.lib` 來編譯，並以連接字串執行，並使用 SQL 查詢（傳回分類的資料行）做為參數：

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

## <a name="bkmk-version"></a>支援的版本
如果 `FieldIdentifier` 設定為 `SQL_CA_SS_DATA_CLASSIFICATION` （1237），Microsoft ODBC 驅動程式17.2 允許透過 `SQLGetDescField` 來抓取資料分類資訊。 

從 Microsoft ODBC Driver 17.4.1.1 開始，您可以使用 `SQL_CA_SS_DATA_CLASSIFICATION_VERSION` （1238）欄位識別碼，透過 `SQLGetDescField` 來抓取伺服器所支援的資料分類版本。 在17.4.1.1 中，支援的資料分類版本設定為 "2"。

 

從17.4.2.1 開始導入了預設版本的資料分類，其設為 "1"，而是將版本驅動程式報告為支援的 SQL Server。 新的連接屬性 `SQL_COPT_SS_DATACLASSIFICATION_VERSION` （1400）可以讓應用程式將支援的資料分類版本從 "1" 變更為支援的最大值。  

範例： 

若要設定此呼叫應該在 SQLConnect 或 SQLDriverConnect 呼叫之前進行的版本：
```
ret = SQLSetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)2, SQL_IS_INTEGER);
```

目前支援的資料分類版本值可透過 SQLGetConnectAttr 呼叫來 retirved： 
```
ret = SQLGetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)&dataClassVersion, SQL_IS_INTEGER, 0);
```

