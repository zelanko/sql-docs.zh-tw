---
title: 大型 CLR 使用者定義型別 (OLE DB) |Microsoft 文件
description: 大型 CLR 使用者定義型別 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: a2b62d0206fc36b69394975f93b7369465edebe1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="large-clr-user-defined-types-ole-db"></a>大型 CLR 使用者定義型別 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題討論 OLE DB 驅動程式以支援大型 common language runtime (CLR) 使用者定義型別 (Udt) 的 SQL Server 中的 OLE DB 的變更。  
  
 如需 SQL Server 的 OLE DB 驅動程式中大型 CLR Udt 支援的詳細資訊，請參閱[Large CLR User-Defined 類型](../../oledb/features/large-clr-user-defined-types.md)。 如需範例，請參閱[使用大型 CLR Udt &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-large-clr-udts-ole-db.md)。  
  
## <a name="data-format"></a>資料格式  
 OLE DB 驅動程式的 SQL Server 會使用 ~ 0 來代表的大型物件 (LOB) 類型的無限制大小的值的長度。 ~0 也代表大於 8,000 個位元組的 CLR UDT 大小。  
  
 下表顯示參數和資料列集內的資料類型對應：  
  
|SQL Server 資料類型|OLE DB 資料類型|記憶體配置|Value|  
|--------------------------|----------------------|-------------------|-----------|  
|CLR UDT|DBTYPE_UDT|BYTE [] （位元組陣列\)|132 (oledb.h)|  
  
 UDT 值會表示為位元組陣列。 支援與十六進位字串之間的來回轉換。 常值會表示為具有 "0x" 前置詞的十六進位字串。 十六進位字串是基底 16 的二進位資料文字表示法。 一個範例就是從伺服器類型轉換**varbinary(10)** 至 DBTYPE_STR，這會導致 20 個字元，其中每一組字元都代表單一位元組的十六進位表示法。  
  
## <a name="parameter-properties"></a>參數屬性  
 DBPROPSET_SQLSERVERPARAMETER 屬性集會透過 OLE DB 支援 UDT。 如需詳細資訊，請參閱[Using User-Defined 類型](../../oledb/features/using-user-defined-types.md)。  
  
## <a name="column-properties"></a>資料行屬性  
 DBPROPSET_SQLSERVERCOLUMN 屬性集會透過 OLE DB 支援資料表的建立。 如需詳細資訊，請參閱[Using User-Defined 類型](../../oledb/features/using-user-defined-types.md)。  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>ITableDefinition::CreateTable 中的資料類型對應  
 下列資訊用於**DBCOLUMNDESC** itabledefinition:: Createtable 需要 UDT 資料行時使用的結構：  
  
|OLE DB 資料類型 (*wType*)|*pwszTypeName*|SQL Server 資料類型|*rgPropertySets*|  
|----------------------------------|--------------------|--------------------------|----------------------|  
|DBTYPE_UDT|忽略|UDT|必須包含 DBPROPSET_SQLSERVERCOLUMN 屬性集。|  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 傳回以 DBPARAMINFO 結構透過資訊**prgParamInfo**如下所示：  
  
|參數類型|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*將 dwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|-------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|"DBTYPE_UDT"|*n*|未定義|未定義|清除|  
|DBTYPE_UDT<br /><br /> (長度大於 8,000 個位元組)|"DBTYPE_UDT"|~0|未定義|未定義|集合|  
  
## <a name="icommandwithparameterssetparameterinfo"></a>ICommandWithParameters::SetParameterInfo  
 以 DBPARAMBINDINFO 結構所提供的資訊必須與下列相符：  
  
|參數類型|*pwszDataSourceType*|*ulParamSize*|*bPrecision*|*bScale*|*將 dwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|--------------------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|DBTYPE_UDT|*n*|忽略|忽略|如果要使用 DBTYPE_IUNKNOWN 傳遞此參數，則必須設定。|  
|DBTYPE_UDT<br /><br /> (長度大於 8,000 個位元組)|DBTYPE_UDT|~0|忽略|忽略|忽略|  
  
## <a name="isscommandwithparameters"></a>ISSCommandWithParameters  
 應用程式使用**ISSCommandWithParameters**取得和設定參數屬性 > 一節中定義的參數屬性。  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 傳回的資料行如下：  
  
|資料行類型|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE|DBCOLUMN_FLAGS_ISLONG|DBCOLUMNS_ISSEARCHABLE|DBCOLUMN_OCTETLENGTH|  
|-----------------|--------------------|--------------------------|-------------------------|---------------------|-----------------------------|-----------------------------|---------------------------|  
|DBTYPE_UDT<br /><br /> (長度小於或等於 8,000 個位元組)|DBTYPE_UDT|*n*|NULL|NULL|Clear|DB_ALL_EXCEPT_LIKE|n|  
|DBTYPE_UDT<br /><br /> (長度大於 8,000 個位元組)|DBTYPE_UDT|~0|NULL|NULL|將|DB_ALL_EXCEPT_LIKE|0|  
  
 下列資料行也會針對 UDT 而定義：  
  
|資料行識別碼|型別|Description|  
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
  
|資料行識別碼|型別|Description|  
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
|DBTYPE_BYTES|支援 (5)|해당 사항 없음|支援 (5)|해당 사항 없음|  
|DBTYPE_WSTR|支援 (2)、(5)|해당 사항 없음|支援 (3)、(5)、(6)|해당 사항 없음|  
|DBTYPE_BSTR|支援 (2)、(5)|해당 사항 없음|支援 (3)、 (5)|해당 사항 없음|  
|DBTYPE_STR|支援 (2)、(5)|해당 사항 없음|支援 (3)、 (5)|해당 사항 없음|  
|DBTYPE_IUNKNOWN|支援 (6)|해당 사항 없음|支援 (6)|해당 사항 없음|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|支援 (5)|해당 사항 없음|支援 (3)、 (5)|해당 사항 없음|  
|DBTYPE_VARIANT (VT_BSTR)|支援 (2)、(5)|해당 사항 없음|不適用|N/A|  
  
### <a name="key-to-symbols"></a>符號的索引鍵  
  
|符號|意義|  
|------------|-------------|  
|1|如果您的伺服器類型與指定了 DBTYPE_UDT 以外**icommandwithparameters:: Setparameterinfo**而且存取子類型為 DBTYPE_UDT，陳述式時發生錯誤。  此錯誤將是 DB_E_ERRORSOCCURRED，而參數狀態將是 DBSTATUS_E_BADACCESSOR。<br /><br /> 針對不是 UDT 的伺服器參數指定 UDT 類型的參數是一項錯誤。|  
|2|資料會從十六進位字串轉換成二進位資料。|  
|3|資料會從二進位資料轉換成十六進位字串。|  
|4|使用時，可能會發生驗證**CreateAccessor**或**GetNextRows**。 錯誤是 DB_E_ERRORSOCCURRED。 繫結狀態設定為 DBBINDSTATUS_UNSUPPORTEDCONVERSION。|  
|5|可能會使用 BY_REF。|  
|6|UDT 參數可以在 DBBINDING 中繫結為 DBTYPE_IUNKNOWN。 繫結至 DBTYPE_IUNKNOWN 表示應用程式想要使用 ISequentialStream 介面資料流形式處理資料。 當取用者指定*wType*繫結為類型 DBTYPE_IUNKNOWN，並對應資料行或輸出中的預存程序的參數是 UDT，OLE DB 驅動程式的 SQL Server 將會傳回 ISequentialStream。 OLE DB 驅動程式的 SQL Server 查詢的輸入參數，如 ISequentialStream 介面。<br /><br /> 在大型 UDT 的情況下，您可以選擇不要在使用 DBTYPE_IUNKNOWN 繫結時繫結 UDT 資料的長度。 不過，小型 UDT 則必須繫結長度。 如果下列其中一項或多項成立，則 DBTYPE_UDT 參數可以指定為大型 UDT：<br />*ulParamParamSize*為 ~ 0。<br />DBPARAMFLAGS_ISLONG 會在 DBPARAMBINDINFO 結構中設定。<br /><br /> 對於資料列資料而言，DBTYPE_IUNKNOWN 繫結只適用於大型 UDT。 您可以找出資料行是否為大型 UDT 類型的資料列集上使用 icolumnsinfo:: Getcolumninfo 方法或命令物件的 IColumnsInfo 介面。 如果下列其中一項或多項成立，則 DBTYPE_UDT 資料行會是大型 UDT 資料行：<br />DBCOLUMNFLAGS_ISLONG 旗標上設定*dwFlags* DBCOLUMNINFO 結構的成員。 <br />*ulColumnSize* DBCOLUMNINFO 的成員為 ~ 0。|  
  
 DBTYPE_NULL 和 DBTYPE_EMPTY 可以針對輸入參數而繫結，但是不能針對輸出參數或結果而繫結。 當針對輸入參數來繫結時，狀態必須針對 DBTYPE_NULL 設定為 DBSTATUS_S_ISNULL，或針對 DBTYPE_EMPTY 設定為 DBSTATUS_S_DEFAULT。 DBTYPE_BYREF 不適用於 DBTYPE_NULL 或 DBTYPE_EMPTY。  
  
 DBTYPE_UDT 也可以轉換成 DBTYPE_EMPTY 或 DBTYPE_NULL。 不過，DBTYPE_NULL 和 DBTYPE_EMPTY 不能轉換成 DBTYPE_UDT。 這與 DBTYPE_BYTES 一致。 **ISSCommandWithParameters**做為參數是用來處理 Udt。  
  
 OLE DB 核心服務所提供的資料轉換 (**IDataConvert**) 不適用於 DBTYPE_UDT。  
  
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
  
 當**DataTypeCompatibility** (SSPROP_INIT_DATATYPECOMPATIBILITY) 設定為"80"，大型 UDT 類型如同它們在下層用戶端會對用戶端。  
  
## <a name="see-also"></a>另請參閱  
 [大型 CLR 使用者定義型別](../../oledb/features/large-clr-user-defined-types.md)  
  
  

