---
title: SSVARIANT 結構 (OLE DB 驅動程式)
description: OLE DB Driver for SQL Server 中的 SSVARIANT 結構
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 701476b8e1cea1f84d7fdbf970a345311d686cfd
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860068"
---
# <a name="ssvariant-structure"></a>SSVARIANT 結構
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  定義於 msoledbsql.h 中的 **SSVARIANT** 結構會對應至 OLE DB Driver for SQL Server 中的 DBTYPE_SQLVARIANT 值。  
  
 **SSVARIANT** 是一個區分集合聯集。 根據 vt 成員的值而定，取用者可以判斷要讀取的成員。 vt 值會對應至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。 因此，**SSVARIANT** 結構可以保留任何 SQL Server 類型。 如需適用於標準 OLE DB 類型之資料結構的詳細資訊，請參閱[類型指示器](https://go.microsoft.com/fwlink/?LinkId=122171) \(英文\)。  
  
## <a name="remarks"></a>備註  
 當 DataTypeCompat==80 時，數個 **SSVARIANT** 子類型會變成字串。 例如，下列 vt 值在 **SSVARIANT** 中會顯示為 VT_SS_WVARSTRING：  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 當 DateTypeCompat == 0 時，這些類型都會以原生形式出現。  
  
 如需 SSPROP_INIT_DATATYPECOMPATIBILITY 的詳細資訊，請參閱[利用 OLE DB Driver for SQL Server 使用連接字串關鍵字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  
  
 msoledbsql.h 檔案包含變數存取巨集，可簡化 **SSVARIANT** 結構中成員類型的取值 (Dereference)。 V_SS_DATETIMEOFFSET 即為一例，可以按照下列方式使用：  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 如需適用於 **SSVARIANT** 結構中每個成員的完整存取巨集集合，請參考 msoledbsql.h 檔案。  
  
 下表將描述 **SSVARIANT** 結構的成員：  
  
|member|OLE DB 類型指標|OLE DB C 資料類型|vt 值|註解|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||指定包含在 **SSVARIANT** 結構中的值類型。|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|支援 **tinyint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|支援 **smallint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|支援 **int**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|支援 **bigint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|支援 **real**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|支援 **float**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|支援 **money** 和 **smallmoney**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|支援 **bit**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|支援 **uniqueidentifier**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|支援 **numeric**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|支援 **date**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|支援 **smalldatetime**、**datetime** 和 **datetime2**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|支援 **time**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。<br /><br /> 包括下列成員：<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**BYTE**) 指定 *tTime2Val* 值的範圍。|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|支援 **datetime2**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。<br /><br /> 包括下列成員：<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**BYTE**) 指定 *tsDataTimeVal* 值的範圍。|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|支援 **datetimeoffset**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。<br /><br /> 包括下列成員：<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**BYTE**) 指定 *tsoDateTimeOffsetVal* 值的範圍。|  
|NCharVal|沒有對應的 OLE DB 類型指標。|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|支援 **nchar** 和 **nvarchar**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。<br /><br /> 包括下列成員：<br /><br /> *sActualLength* (**SHORT**) 指定 *pwchNCharVal* 指向之字串的實際長度。 不包括結尾的零。<br /><br /> *sMaxLength* (**SHORT**) 指定 *pwchNCharVal* 指向之字串的最大長度。<br /><br /> *pwchNCharVal* (**WCHAR** \*) 指向字串的指標。<br /><br /> *rgbReserved* (**BYTE[5]** ) 指定定序資訊。<br /><br /> 未使用的成員：*dwReserved* 及 *pwchReserved*。|  
|CharVal|沒有對應的 OLE DB 類型指標。|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|支援 **char** 和 **varchar**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。<br /><br /> 包括下列成員：<br /><br /> *sActualLength* (**SHORT**) 指定 *pchCharVal* 指向之字串的實際長度。 不包括結尾的零。<br /><br /> *sMaxLength* (**SHORT**) 指定 *pchCharVal* 指向之字串的最大長度。<br /><br /> *pchCharVal* (**CHAR** \*) 指向字串的指標。<br /><br /> *rgbReserved* (**BYTE[5]** ) 指定定序資訊。<br /><br /> 未使用的成員：<br /><br /> *dwReserved* 及 *pwchReserved*。|  
|BinaryVal|沒有對應的 OLE DB 類型指標。|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|支援 **binary** 和 **varbinary**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。<br /><br /> 包括下列成員：<br /><br /> *sActualLength* (**SHORT**) 指定 *prgbBinaryVal* 指向之資料的實際長度。<br /><br /> *sMaxLength* (**SHORT**) 指定 *prgbBinaryVal* 指向之資料的最大長度。<br /><br /> *prgbBinaryVal* (**BYTE** \*) 指向二進位資料的指標。<br /><br /> 未使用的成員：*dwReserved*。|  
|UnknownType|未使用|未使用|未使用|未使用|  
|BLOBType|未使用|未使用|未使用|未使用|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
  
## <a name="known-issues"></a>已知問題
### <a name="possible-narrow-string-data-corruption"></a>可能的窄字串資料損毀
在 OLE DB 驅動程式 18.4 版之前，若下列所有條件都成立，則 `sql_variant` 資料行中的插入可能會導致伺服器上的資料損毀：
- 用戶端電腦字碼頁不符合資料庫定序字碼頁。
- 要插入的用戶端緩衝區，包含以用戶端字碼頁編碼的非 ASCII 窄字串字元。
- 若下列其中一項條件成立：
  - `DBPARAMBINDINFO` 結構中的 `pwszDataSourceType` 欄位，其描述對應至 `sql_variant` 資料行的參數已設定為 `L"DBTYPE_SQLVARIANT"`、`L"DBTYPE_VARIANT"` 或 `L"sql_variant"`。 如需詳細資料，請參閱：[ICommandWithParameters::SetParameterInfo](https://docs.microsoft.com/previous-versions/windows/desktop/ms725393(v=vs.85))。

    *or*
  - 用於插入的參數化 SQL 查詢已準備妥當。

更明確的說，OLE DB 驅動程式不會在插入資料之前，將其翻譯成資料庫定序字碼頁。 然而，此驅動程式錯誤地向伺服器指出，資料庫定序字碼頁中的資料已編碼。 此行為導致資料與其儲存在 `sql_variant` 欄中的對應字碼頁不相符。

同樣地，在擷取相同的值時，OLE DB 驅動程式不會將字串翻譯成用戶端字碼頁。 然而，由於插入的資料已經在用戶端字碼頁中 (請參閱上面的段落)，因此用戶端應用程式可正確地解譯資料。 就算如此，使用其他驅動程式的應用程式，也會以損毀的格式擷取這些值。 會發生損毀是因為其他驅動程式在資料庫定序字碼頁中解譯了字串，並嘗試將其翻譯成用戶端字碼頁。

自 18.4 版起，OLE DB Driver 會在插入之前，將窄字串翻譯成資料庫定序字碼頁。 同樣地，驅動程式也會在擷取時，將資料翻譯回用戶端字碼頁。 因此，依賴上述 Bug 的用戶端應用程式，可能會在擷取使用舊版 OLE DB Driver 插入的資料時遇到問題。 下方[復原程序](#recovery-procedure)旨在提供解決這些問題的指引。

### <a name="recovery-procedure"></a>復原程序
> [!IMPORTANT]  
> 執行下列復原步驟之前，請務必備份現有的資料。

若應用程式在切換至 OLE DB 驅動程式 18.4 版之後，在從 `sql_variant` 資料行擷取資料時遇到問題，則必須修改損毀的資料，使其定序與儲存資料的資料庫相同。 下列指令碼可用來從 `sql_variant` 資料行復原單一值。 指令碼是範本，必須加以調整以符合情況。

> [!IMPORTANT]  
> 由於不會儲存資料的原始字碼頁，因此必須告知伺服器初始如何編碼資料。 若要執行這項操作，請在資料庫的內容中執行指令碼，其字碼頁與初始插入資料的用戶端其字碼頁相同。 例如，若從使用字碼頁 `932` 所設定用戶端插入損毀的資料，則必須在具有日文定序的資料庫內容 (例如 `Japanese_XJIS_100_CS_AI`) 中執行下列指令碼。

```sql
/*
    Description:
        Template that can be used to recover the corrupted value inserted into the sql_variant column.

    Scenario:
        The database is named [YourDatabase] and it contains a table named [YourTable], which contains the corrupted value.
        Schema is named [dbo].
        The corrupted value is stored in a column of type sql_variant named [YourColumn].
        The corrupted value is sql_variant of BaseType char. For details on sql_variant properties, see:
            https://docs.microsoft.com/sql/t-sql/functions/sql-variant-property-transact-sql
*/

-- Base type in sql_variant can hold a maximum of 8000 bytes
-- For details see: 
--  https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql#remarks
DECLARE @bin VARBINARY(8000)

-- In the following lines we convert the sql_variant base type to binary.
-- <FilterExpression>
--      Is a placeholder and must be replaced with an expression that filters a single corrupted value to be recovered.
--      Therefore, the expression must result in a single value being returned only.
SET @bin = (SELECT CAST([YourColumn] AS VARBINARY(8000)) FROM [YourDatabase].[dbo].[YourTable] WHERE <FilterExpression>)

-- In the following lines we store the binary value in char(59) (a fixed-size character data type).
-- IMPORTANT NOTE: 
--      This example assumes the corrupted sql_variant's base type is char(59).
--      You MUST adjust the type (that is, char/varchar) and size to match your scenario exactly.
DECLARE @char CHAR(59)
SET @char = CAST((@bin) AS CHAR(59))
DECLARE @sqlvariant sql_variant

-- The following lines recover the corrupted value by translating the value to the collation of the database.
-- <DBCollation>
--      Must be replaced with the collation (for example, Latin1_General_100_CI_AS_SC_UTF8) of the database holding the data.
SET @sqlvariant = @char collate <DBCollation>

-- Finally, we update the corrupted value with the recovered value.
-- "<FilterExpression>"
--      Is a placeholder and must be replaced with an expression that filters a single corrupted value to be recovered.
--      Therefore, the expression must result in a single value being returned only.
UPDATE [YourDatabase].[dbo].[YourTable] SET [YourColumn] = @sqlvariant WHERE <FilterExpression>
```

## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
