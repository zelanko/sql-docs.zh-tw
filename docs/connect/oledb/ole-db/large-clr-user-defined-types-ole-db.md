---
title: 大型 CLR 使用者定義類型 (OLE DB) |Microsoft Docs
description: 大型 CLR 使用者定義型別 (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 228054b56d6b26bf4439c01363d6cad24422f938
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015217"
---
# <a name="large-clr-user-defined-types-ole-db"></a>大型 CLR 使用者定義型別 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本主題討論 OLE DB Driver for SQL Server 中 OLE DB 的變更，以支援大型 Common Language Runtime (CLR) 使用者定義型別 (UDT)。  
  
 如需在 SQL Server 的 OLE DB 驅動程式中支援大型 CLR Udt 的詳細資訊, 請參閱[大型 Clr 使用者定義型](../../oledb/features/large-clr-user-defined-types.md)別。 如需範例, 請參閱[使用大型 CLR &#40;udt&#41;OLE DB](../../oledb/ole-db-how-to/use-large-clr-udts-ole-db.md)。  
  
## <a name="data-format"></a>資料格式  
 OLE DB Driver for SQL Server 使用 ~0 來代表大型物件 (LOB) 類型的無限制大小的值長度。 ~0 也代表大於 8,000 個位元組的 CLR UDT 大小。  
  
 下表顯示參數和資料列集內的資料類型對應：  
  
|SQL Server 資料類型|OLE DB 資料類型|記憶體配置|ReplTest1|  
|--------------------------|----------------------|-------------------|-----------|  
|CLR UDT|DBTYPE_UDT|BYTE[](位元組陣列\)|132 (oledb.h)|  
  
 UDT 值會表示為位元組陣列。 支援與十六進位字串之間的來回轉換。 常值會表示為具有 "0x" 前置詞的十六進位字串。 十六進位字串是基底 16 的二進位資料文字表示法。 從伺服器類型 **varbinary(10)** 轉換成 DBTYPE_STR 即為此類範例，這項作業會得出 20 個字元的十六進位表示，其中每一組字元都代表單一位元組。  
  
## <a name="parameter-properties"></a>參數屬性  
 DBPROPSET_SQLSERVERPARAMETER 屬性集會透過 OLE DB 支援 UDT。 如需詳細資訊，請參閱[使用使用者定義型別](../../oledb/features/using-user-defined-types.md)。  
  
## <a name="column-properties"></a>資料行屬性  
 DBPROPSET_SQLSERVERCOLUMN 屬性集會透過 OLE DB 支援資料表的建立。 如需詳細資訊，請參閱[使用使用者定義型別](../../oledb/features/using-user-defined-types.md)。  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>ITableDefinition::CreateTable 中的資料類型對應  
 當需要 UDT 資料行時，下列資訊會用於 ITableDefinition::CreateTable 所使用的 **DBCOLUMNDESC** 結構中：  
  
|OLE DB 資料類型 (*wType*)|*pwszTypeName*|SQL Server 資料類型|*rgPropertySets*|  
|----------------------------------|--------------------|--------------------------|----------------------|  
|DBTYPE_UDT|忽略|UDT|必須包含 DBPROPSET_SQLSERVERCOLUMN 屬性集。|  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 透過 **prgParamInfo** 以 DBPARAMINFO 結構所傳回的資訊如下：  
  
|參數類型|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|-------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|"DBTYPE_UDT"|*n*|未定義|未定義|清除|  
|DBTYPE_UDT<br /><br /> (長度大於 8,000 個位元組)|"DBTYPE_UDT"|~0|未定義|未定義|集合|  
  
## <a name="icommandwithparameterssetparameterinfo"></a>ICommandWithParameters::SetParameterInfo  
 以 DBPARAMBINDINFO 結構所提供的資訊必須與下列相符：  
  
|參數類型|*pwszDataSourceType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|--------------------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|DBTYPE_UDT|*n*|忽略|忽略|如果要使用 DBTYPE_IUNKNOWN 傳遞此參數，則必須設定。|  
|DBTYPE_UDT<br /><br /> (長度大於 8,000 個位元組)|DBTYPE_UDT|~0|忽略|忽略|忽略|  
  
## <a name="isscommandwithparameters"></a>ISSCommandWithParameters  
 應用程式會使用 **ISSCommandWithParameters** 來取得並設定定義於 Parameter Properties 區段中的參數屬性。  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 傳回的資料行如下：  
  
|資料行類型|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE|DBCOLUMN_FLAGS_ISLONG|DBCOLUMNS_ISSEARCHABLE|DBCOLUMN_OCTETLENGTH|  
|-----------------|--------------------|--------------------------|-------------------------|---------------------|-----------------------------|-----------------------------|---------------------------|  
|DBTYPE_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|DBTYPE_UDT|*n*|NULL|NULL|Clear|DB_ALL_EXCEPT_LIKE|n|  
|DBTYPE_UDT<br /><br /> (長度大於 8,000 個位元組)|DBTYPE_UDT|~0|NULL|NULL|將|DB_ALL_EXCEPT_LIKE|0|  
  
 下列資料行也會針對 UDT 而定義：  
  
|資料行識別碼|類型|Description|  
|-----------------------|----------|-----------------|  
|DBCOLUMN_UDT_CATALOGNAME|DBTYPE_WSTR|對於 UDT 資料行而言，此為定義 UDT 之目錄的名稱。|  
|DBCOLUMN_UDT_SCHEMANAME|DBTYPE_WSTR|對於 UDT 資料行而言，此為定義 UDT 之結構描述的名稱。|  
|DBCOLUMN_UDT_NAME|DBTYPE_WSTR|對於 UDT 資料行而言，此為 UDT 的單一部分名稱。|  
|DBCOLUMN_ASSEMBLY_TYPENAME|DBTYPE_WSTR|對於 UDT 資料行而言，此為 UDT 的完整類型名稱。 組件類型的完整名稱可以讓您使用 Type.GetType 方法來具現化該類型的物件。|  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 以 DBCOLUMNINFO 結構所傳回的資訊如下：  
  
|參數類型|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBCOLUMNFLAGS_ISLONG|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------|  
|DBTYPE_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|DBTYPE_UDT|*n*|~0|~0|Clear|  
|DBTYPE_UDT<br /><br /> (長度大於 8,000 個位元組)|DBTYPE_UDT|~0|~0|~0|將|  
  
## <a name="columns-rowset-schema-rowsets"></a>COLUMNS 資料列集 (結構描述資料列集)  
 下列資料行值是針對 UDT 類型所傳回：  
  
|資料行類型|DATA_TYPE|COLUMN_FLAGS、DBCOLUMFLAGS_ISLONG|CHARACTER_OCTET_LENGTH|  
|-----------------|----------------|-----------------------------------------|------------------------------|  
|DBTYPE_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|DBTYPE_UDT|Clear|*n*|  
|DBTYPE_UDT<br /><br /> (長度大於 8,000 個位元組)|DBTYPE_UDT|將|0|  
  
 下列其他資料行也會針對 UDT 而定義：  
  
|資料行識別碼|類型|Description|  
|-----------------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|對於 UDT 資料行而言，此為定義 UDT 之目錄的名稱。|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|對於 UDT 資料行而言，此為定義 UDT 之結構描述的名稱。|  
|SS_UDT_NAME|DBTYPE_WSTR|對於 UDT 資料行而言，此為 UDT 的單一部分名稱。|  
|SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|對於 UDT 資料行而言，此為 UDT 的完整類型名稱。 組件類型的完整名稱可以讓您使用 Type.GetType 方法來具現化該類型的物件。|  
  
 有關 PROCEDURE_PARAMETERS 資料列集方面，DATA_TYPE 會包含與 COLUMNS 結構描述資料列集相同的值，而 TYPE_NAME 則會包含 UDT。 也會定義相同的其他資料行。  
  
 使用者定義型別不會出現在 PROVIDER_TYPES 結構描述資料列集中。  
  
## <a name="bindings-and-conversions"></a>繫結和轉換  
  
|繫結資料類型|UDT 到伺服器|非 UDT 到伺服器|從伺服器中的 UDT|從伺服器中的非 UDT|  
|----------------------|-------------------|------------------------|---------------------|--------------------------|  
|DBTYPE_UDT|支援 (5)|錯誤 (1)|支援 (5)|錯誤 (4)|  
|DBTYPE_BYTES|支援 (5)|不適用|支援 (5)|不適用|  
|DBTYPE_WSTR|支援 (2)、(5)|不適用|支援 (3)、(5)、(6)|不適用|  
|DBTYPE_BSTR|支援 (2)、(5)|不適用|支援 (3)、(5)|不適用|  
|DBTYPE_STR|支援 (2)、(5)|不適用|支援 (3)、(5)|不適用|  
|DBTYPE_IUNKNOWN|支援 (6)|不適用|支援 (6)|不適用|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|支援 (5)|不適用|支援 (3)、(5)|不適用|  
|DBTYPE_VARIANT (VT_BSTR)|支援 (2)、(5)|不適用|不適用|不適用|  
  
### <a name="key-to-symbols"></a>符號的索引鍵  
  
|符號|意義|  
|------------|-------------|  
|1|如果使用 **ICommandWithParameters::SetParameterInfo** 指定 DBTYPE_UDT 以外的伺服器類型，而且存取子類型為 DBTYPE_UDT，則當陳述式執行時會發生錯誤。  此錯誤將是 DB_E_ERRORSOCCURRED，而參數狀態將是 DBSTATUS_E_BADACCESSOR。<br /><br /> 針對不是 UDT 的伺服器參數指定 UDT 類型的參數是一項錯誤。|  
|2|資料會從十六進位字串轉換成二進位資料。|  
|3|資料會從二進位資料轉換成十六進位字串。|  
|4|在使用 **CreateAccessor** 或 **GetNextRows** 時可能會發生驗證。 錯誤是 DB_E_ERRORSOCCURRED。 繫結狀態設定為 DBBINDSTATUS_UNSUPPORTEDCONVERSION。|  
|5|可能會使用 BY_REF。|  
|6|UDT 參數可以在 DBBINDING 中繫結為 DBTYPE_IUNKNOWN。 繫結至 DBTYPE_IUNKNOWN 表示應用程式想要使用 ISequentialStream 介面將資料處理為資料流。 當取用者在系結中將*wType*指定為類型 DBTYPE_IUNKNOWN, 而預存程式的對應資料行或輸出參數為 UDT 時, SQL Server 的 OLE DB 驅動程式會傳回 ISequentialStream。 針對輸入參數, SQL Server 的 OLE DB 驅動程式會查詢 ISequentialStream 介面的。<br /><br /> 在大型 UDT 的情況下，您可以選擇不要在使用 DBTYPE_IUNKNOWN 繫結時繫結 UDT 資料的長度。 不過，小型 UDT 則必須繫結長度。 如果下列其中一項或多項成立，則 DBTYPE_UDT 參數可以指定為大型 UDT：<br />*ulParamParamSize*為 ~ 0。<br />DBPARAMFLAGS_ISLONG 會在 DBPARAMBINDINFO 結構中設定。<br /><br /> 對於資料列資料而言，DBTYPE_IUNKNOWN 繫結只適用於大型 UDT。 您可以使用資料列集或命令物件的 IColumnsInfo 介面上的 IColumnsInfo:: GetColumnInfo 方法, 找出資料行是否為大型的 UDT 類型。 如果下列其中一項或多項成立，則 DBTYPE_UDT 資料行會是大型 UDT 資料行：<br />DBCOLUMNFLAGS_ISLONG 旗標會在 DBCOLUMNINFO 結構的 *dwFlags* 成員上設定。 <br />DBCOLUMNINFO 的*ulColumnSize*成員為 ~ 0。|  
  
 DBTYPE_NULL 和 DBTYPE_EMPTY 可以針對輸入參數而繫結，但是不能針對輸出參數或結果而繫結。 當針對輸入參數來繫結時，狀態必須針對 DBTYPE_NULL 設定為 DBSTATUS_S_ISNULL，或針對 DBTYPE_EMPTY 設定為 DBSTATUS_S_DEFAULT。 DBTYPE_BYREF 不適用於 DBTYPE_NULL 或 DBTYPE_EMPTY。  
  
 DBTYPE_UDT 也可以轉換成 DBTYPE_EMPTY 或 DBTYPE_NULL。 不過，DBTYPE_NULL 和 DBTYPE_EMPTY 不能轉換成 DBTYPE_UDT。 這與 DBTYPE_BYTES 一致。 **ISSCommandWithParameters** 可用來將 UDT 當作參數處理。  
  
 OLE DB 核心服務 (**IDataConvert**) 提供的資料轉換不適用於 DBTYPE_UDT。  
  
 不支援其他任何繫結。  
  
## <a name="comparability-for-irowsetfind"></a>IRowsetFind 的相容性  
 對於 UDT 類型而言，只支援下列比較：  
  
-   EQ  
  
-   NE  
  
-   IGNORE  
  
 如果嘗試其他任何比較，就會傳回 DB_E_BADCOMPAREOP。  
  
## <a name="bcp-support-for-udts"></a>UDT 的 BCP 支援  
 UDT 值只能當做字元或二進位值來匯入及匯出。  
  
## <a name="down-level-client-behavior-for-udts"></a>UDT 的下層用戶端行為  
 UDT 受限於與下層用戶端對應的類型，如下所示：  
  
|用戶端版本|DBTYPE_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|DBTYPE_UDT<br /><br /> (長度大於 8,000 個位元組)|  
|--------------------|------------------------------------------------------------------|---------------------------------------------------------|  
|SQL Server 2005|UDT|varbinary(max)|  
|SQL Server 2008 及更新版本|UDT|UDT|  
  
 當 **DataTypeCompatibility** (SSPROP_INIT_DATATYPECOMPATIBILITY) 設定為 "80" 時，大型 UDT 類型會以針對下層用戶端顯示的方式向用戶端顯示。  
  
## <a name="see-also"></a>另請參閱  
 [大型 CLR 使用者定義型別](../../oledb/features/large-clr-user-defined-types.md)  
  
  

