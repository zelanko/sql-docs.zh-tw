---
title: SQLColAttribute |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColAttribute function
ms.assetid: a5387d9e-a243-4cfe-b786-7fad5842b1d6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1bb59a18dfd0a2952f3c5f23be9d0c12d9c35fd3
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51657438"
---
# <a name="sqlcolattribute"></a>SQLColAttribute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  您可以使用**SQLColAttribute**來擷取已備妥或已執行的 ODBC 陳述式的結果集資料行的屬性。 呼叫**SQLColAttribute**上備妥陳述式造成的往返[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會接收結果集資料行資料做為陳述式執行，因此，呼叫的一部分**SQLColAttribute**完成後**SQLExecute**或**SQLExecDirect**不造成伺服器往返。  
  
> [!NOTE]  
>  ODBC 資料行識別碼屬性並非在所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 結果集上都有提供。  
  
|欄位識別碼|描述|  
|----------------------|-----------------|  
|SQL_COLUMN_TABLE_NAME|可用於擷取自產生伺服器資料指標之陳述式的結果集，或包含 FOR BROWSE 子句之已執行 SELECT 陳述式。|  
|SQL_DESC_BASE_COLUMN_NAME|可用於擷取自產生伺服器資料指標之陳述式的結果集，或包含 FOR BROWSE 子句之已執行 SELECT 陳述式。|  
|SQL_DESC_BASE_TABLE_NAME|可用於擷取自產生伺服器資料指標之陳述式的結果集，或包含 FOR BROWSE 子句之已執行 SELECT 陳述式。|  
|SQL_DESC_CATALOG_NAME|資料庫名稱。 可用於擷取自產生伺服器資料指標之陳述式的結果集，或包含 FOR BROWSE 子句之已執行 SELECT 陳述式。|  
|SQL_DESC_LABEL|可用於所有結果集上。 此值與 SQL_DESC_NAME 欄位的值相同。<br /><br /> 只有在資料行為運算式的結果，而且運算式不包含標籤指派時，欄位的長度才為零。|  
|SQL_DESC_NAME|可用於所有結果集上。 此值與 SQL_DESC_LABEL 欄位的值相同。<br /><br /> 只有在資料行為運算式的結果，而且運算式不包含標籤指派時，欄位的長度才為零。|  
|SQL_DESC_SCHEMA_NAME|擁有者名稱。 可用於擷取自產生伺服器資料指標之陳述式的結果集，或包含 FOR BROWSE 子句之已執行 SELECT 陳述式。<br /><br /> 只有在 SELECT 陳述式中針對資料行指定擁有者名稱時才適用。|  
|SQL_DESC_TABLE_NAME|可用於擷取自產生伺服器資料指標之陳述式的結果集，或包含 FOR BROWSE 子句之已執行 SELECT 陳述式。|  
|SQL_DESC_UNNAMED|除非資料行是運算式的結果，而且該運算式在執行時不包含標籤指派，否則為結果集中所有資料行的 SQL_NAMED。 當 SQL_DESC_UNNAMED 傳回 SQL_UNNAMED 時，資料行的所有 ODBC 資料行識別碼屬性都包含零長度字串。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會使用 SET FMTONLY 陳述式來減少伺服器的負擔時**SQLColAttribute**會針對備妥但未執行的陳述式呼叫。  
  
 對於大數值類型**SQLColAttribute**會傳回下列值：  
  
|欄位識別碼|變更的描述|  
|----------------------|---------------------------|  
|SQL_DESC_DISPLAY_SIZE|這是從資料行顯示資料所需的最大字元數。 對於大數值類型資料行，傳回的值為 SQL_SS_LENGTH_UNLIMITED。|  
|SQL_DESC_LENGTH|傳回結果集中資料行的實際長度。 對於大數值類型資料行，傳回的值為 SQL_SS_LENGTH_UNLIMITED。|  
|SQL_DESC_OCTET_LENGTH|傳回大數值類型資料行的最大長度。 SQL_SS_LENGTH_UNLIMITED 用來表示無限制的大小。|  
|SQL_DESC_PRECISION|對於大數值類型資料行，傳回 SQL_SS_LENGTH_UNLIMITED 值。|  
|SQL_DESC_TYPE|對於大數值類型，傳回 SQL_VARCHAR, SQL_WVARCHAR 和 SQL_VARBINARY。|  
|SQL_DESC_TYPE_NAME|對於大數值類型，傳回 "varchar"、"varbinary"、"nvarchar"。|  
  
 對於所有版本，當已備妥的 SQL 陳述式批次產生多個結果集時，只有第一個結果集會報告資料行屬性。  
  
 下列資料行屬性是公開的延伸模組[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式傳回所有的值，以*Numericattrptr&lt*參數。 除了 SQL_CA_SS_COMPUTE_BYLIST (WORD 陣列的指標) 之外，這些值會當做 SDWORD (signed long) 傳回。  
  
|欄位識別碼|傳回的值|  
|----------------------|--------------------|  
|SQL_CA_SS_COLUMN_HIDDEN*|如果參考的資料行是針對支援包含 FOR BROWSE 之 Transact-SQL SELECT 陳述式所建立的隱藏主索引鍵一部分，則為 TRUE。|  
|SQL_CA_SS_COLUMN_ID|在目前的 Transact-SQL SELECT 陳述式中，COMPUTE 子句結果資料行的序數位置。|  
|SQL_CA_SS_COLUMN_KEY*|如果參考的資料行是資料列的主索引鍵一部分，而且 Transact-SQL SELECT 陳述式包含 FOR BROWSE，則為 TRUE。|  
|SQL_CA_SS_COLUMN_OP|指定在 COMPUTE 子句資料行中負責值之彙總運算子的整數。 整數值的定義位於 sqlncli.h。|  
|SQL_CA_SS_COLUMN_ORDER|在 ODBC 或 Transact-SQL SELECT 陳述式的 ORDER BY 子句中，資料行的序數位置。|  
|SQL_CA_SS_COLUMN_SIZE|將擷取自資料行的資料值繫結至 SQL_C_BINARY 變數的最大長度 (以位元組為單位)。|  
|SQL_CA_SS_COLUMN_SSTYPE|儲存在 SQL Server 資料行中之資料的原生資料類型。 類型值的定義位於 sqlncli.h。|  
|SQL_CA_SS_COLUMN_UTYPE|SQL Server 資料行之使用者定義資料類型的基底資料類型。 類型值的定義位於 sqlncli.h。|  
|SQL_CA_SS_COLUMN_VARYLEN|如果資料行的資料長度可以改變，則為 TRUE，否則為 FALSE。|  
|SQL_CA_SS_COMPUTE_BYLIST|WORD (unsigned short) 陣列的指標，指定在 COMPUTE 子句之 BY 片語中所使用的資料行。 如果 COMPUTE 子句沒有指定 BY 片語，則會傳回 NULL 指標。<br /><br /> 陣列的第一個元素包含 BY 清單資料行的計數。 其他元素為資料行序數。|  
|SQL_CA_SS_COMPUTE_ID|*computeid*中目前的 TRANSACT-SQL SELECT 陳述式的 COMPUTE 子句結果資料列。|  
|SQL_CA_SS_NUM_COMPUTES|在目前的 Transact-SQL SELECT 陳述式中指定的 COMPUTE 子句數目。|  
|SQL_CA_SS_NUM_ORDERS|在 ODBC 或 Transact-SQL SELECT 陳述式的 ORDER BY 子句中指定之資料行的數目。|  
  
 \*   如果陳述式屬性 SQL_SOPT_SS_HIDDEN_COLUMNS 設定為 sql_hc_on 時，可用。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 導入驅動程式專屬描述項欄位來提供其他資訊，分別代表 XML 結構描述集合名稱、 結構描述名稱，以及目錄名稱。 如果這些屬性包含非英數字元，則它們不需要引號或逸出字元。 下表列出這些新的描述項欄位：  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME|CharacterAttributePtr|定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。<br /><br /> 此資訊會從 IRD 的 SQL_DESC_SS_XML_SCHEMACOLLECTION_CATALOG_NAME 記錄欄位傳回，該欄位為唯讀欄位。|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAM E|CharacterAttributePtr|定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，則此變數包含空字串。<br /><br /> 此資訊會從 IRD 的 SQL_DESC_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME 記錄欄位傳回，該欄位為唯讀欄位。|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_NAME|CharacterAttributePtr|XML 結構描述集合的名稱。 如果找不到名稱，則此變數包含空字串。<br /><br /> 此資訊會從 IRD 的 SQL_DESC_SS_XML_SCHEMACOLLECTION_NAME 記錄欄位傳回，該欄位為唯讀欄位。|  
  
 同時，[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 推出新的驅動程式專屬描述項欄位，針對結果集的使用者定義型別 (UDT) 資料行或預存程序或參數化查詢的 UDT 參數，提供額外的資訊。 如果這些屬性包含非英數字元，則它們不需要引號或逸出字元。 下表列出這些新的描述項欄位：  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_UDT_CATALOG_NAME|CharacterAttributePtr|包含 UDT 之目錄的名稱。|  
|SQL_CA_SS_UDT_SCHEMA_NAME|CharacterAttributePtr|包含 UDT 之結構描述的名稱。|  
|SQL_CA_SS_UDT_TYPE_NAME|CharacterAttributePtr|UDT 的名稱。|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|CharacterAttributePtr|UDT 的組件完整名稱。|  
  
 現有的描述項欄位識別碼 SQL_DESC_TYPE_NAME 用來表示 UDT 的名稱。 適用於 UDT 類型資料行的 SQL_DESC_TYPE 欄位為 SQL_SS_UDT。  
  
## <a name="sqlcolattribute-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLColAttribute 支援  
 針對日期/時間類型傳回的值，請參閱 「 資訊 IRD 欄位中傳回 」 一節[參數和結果中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 日期和時間改善&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。</c0>  
  
## <a name="sqlcolattribute-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLColAttribute 支援  
 **SQLColAttribute**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱 < [Large CLR User-Defined 類型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlcolattribute-support-for-sparse-columns"></a>疏鬆資料行的 SQLColAttribute 支援  
 SQLColAttribute 查詢新實作資料列描述項 (IRD) 欄位 SQL_CA_SS_IS_COLUMN_SET 來判斷資料行是否**column_set**資料行。  
  
 如需詳細資訊，請參閱 <<c0> [ 疏鬆資料行支援&#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [SQLColAttribute 函數](https://go.microsoft.com/fwlink/?LinkId=59334)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
  
