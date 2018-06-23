---
title: 使用使用者定義型別 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_DATASOURCEINFO property set
- UDTs [SQL Server Native Client]
- user-defined types [SQL Server], SQL Server Native Client
- SQL Server Native Client OLE DB provider, user-defined types
- DBPROPSET_SQLSERVERPARAMETER property set
- IColumnsRowset interface
- SQLNCLI, user-defined types
- SQL Server Native Client, user-defined types
- data access [SQL Server Native Client], user-defined types
- ISSCommandWithParameters interface
ms.assetid: e15d8169-3517-4323-9c9e-0f5c34aff7df
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: eaa97c4322c59c0ffc77f42cfe9e147ca7dc276b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133493"
---
# <a name="using-user-defined-types"></a>使用使用者定義型別
  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 導入了使用者定義型別 (UDT)。 Udt 會擴充 SQL 類型系統，可讓您將物件和自訂資料結構中的儲存[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫。 UDT 可以包含多個資料類型並可以具有行為，使其有別於由單一 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系統資料類型組成的傳統別名資料類型。 UDT 是使用會產生可驗證程式碼之 .NET Common Language Runtime (CLR) 支援的任何語言所定義。 這包括 Microsoft Visual C#<sup>®</sup>和 Visual Basic<sup>®</sup> .NET。 資料會公開為 .NET 類別或結構的欄位及屬性，並且其行為是由類別或結構的方法來定義。  
  
 UDT 可用做資料表的資料行定義中的變數[!INCLUDE[tsql](../../../includes/tsql-md.md)]批次，或做為引數的[!INCLUDE[tsql](../../../includes/tsql-md.md)]函式或預存程序。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 提供者  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援使用 Udt 當做具有中繼資料資訊，可讓您管理 Udt 當做物件的二進位類型。 UDT 資料行公開為 DBTYPE_UDT，而且它們的中繼資料會公開透過核心 OLE DB 介面**IColumnRowset**，與新[ISSCommandWithParameters](../../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)介面。  
  
> [!NOTE]  
>  **Irowsetfind:: Findnextrow**方法不適用於 UDT 資料類型。 如果將 UDT 當做搜尋資料行類型使用，就會傳回 DB_E_BADCOMPAREOP。  
  
### <a name="data-bindings-and-coercions"></a>資料繫結和強制型轉  
 下表描述當搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] UDT 使用列出的資料類型時，所發生的繫結和強制型轉。 UDT 資料行透過公開[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]DBTYPE_UDT Native Client OLE DB 提供者。 您可以透過適當的結構描述資料列集來取得中繼資料，好讓您可以將自己定義的類型當做物件來管理。  
  
|資料類型|到伺服器<br /><br /> **UDT**|到伺服器<br /><br /> **non-UDT**|從伺服器<br /><br /> **UDT**|從伺服器<br /><br /> **non-UDT**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|支援<sup>6</sup>|錯誤<sup>1</sup>|支援<sup>6</sup>|錯誤<sup>5</sup>|  
|DBTYPE_BYTES|支援<sup>6</sup>|N/A<sup>2</sup>|支援<sup>6</sup>|N/A<sup>2</sup>|  
|DBTYPE_WSTR|支援<sup>3、 6</sup>|N/A<sup>2</sup>|支援<sup>4、 6</sup>|N/A<sup>2</sup>|  
|DBTYPE_BSTR|支援<sup>3、 6</sup>|N/A<sup>2</sup>|支援<sup>4</sup>|N/A<sup>2</sup>|  
|DBTYPE_STR|支援<sup>3、 6</sup>|N/A<sup>2</sup>|支援<sup>4、 6</sup>|N/A<sup>2</sup>|  
|DBTYPE_IUNKNOWN|不支援|N/A<sup>2</sup>|不支援|N/A<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &AMP;#124; VT_ARRAY)|支援<sup>6</sup>|N/A<sup>2</sup>|支援<sup>4</sup>|N/A<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|支援<sup>3、 6</sup>|N/A<sup>2</sup>|不適用|N/A<sup>2</sup>|  
  
 <sup>1</sup>如果的伺服器類型與指定了 DBTYPE_UDT 以外**icommandwithparameters:: Setparameterinfo**而且存取子類型為 DBTYPE_UDT，陳述式執行時，就會發生錯誤 (DB_E_ERRORSOCCURRED;參數狀態為 DBSTATUS_E_BADACCESSOR）。 否則資料會傳給伺服器，但是伺服器會傳回一則錯誤，指示從 UDT 到參數的資料類型之間沒有隱含轉換。  
  
 <sup>2</sup>超出本主題的範圍。  
  
 <sup>3</sup>十六進位字串的資料轉換成二進位資料，就會發生。  
  
 <sup>4</sup>發生從十六進位字串的二進位資料轉換的資料轉換。  
  
 <sup>5</sup>可能發生驗證建立存取子時，或提取時，錯誤為 DB_E_ERRORSOCCURRED，繫結狀態設定為 DBBINDSTATUS_UNSUPPORTEDCONVERSION。  
  
 <sup>6</sup>可能會使用 BY_REF。  
  
 可以繫結 DBTYPE_NULL 和 DBTYPE_EMPTY 用於輸入參數，但是不能用於輸出參數或結果。 當針對輸入參數來繫結時，狀態必須設定為 DBSTATUS_S_ISNULL 或 DBSTATUS_S_DEFAULT。  
  
 DBTYPE_UDT 也可以轉換成 DBTYPE_EMPTY 和 DBTYPE_NULL，但是 DBTYPE_NULL 和 DBTYPE_EMPTY 無法轉換成 DBTYPE_UDT。 這與 DBTYPE_BYTES 一致。  
  
> [!NOTE]  
>  新的介面來處理 Udt 做為參數， **ISSCommandWithParameters**，後者繼承自**ICommandWithParameters**。 應用程式必須使用這個介面，至少為 UDT 參數設定 DBPROPSET_SQLSERVERPARAMETER 屬性集的 SSPROP_PARAM_UDT_NAME。 如果不這麼做， **icommand:: Execute**將會傳回 DB_E_ERRORSOCCURRED。 本主題稍後將描述這個介面和屬性集。  
  
 如果使用者定義型別插入的資料行不夠大，無法保留所有資料， **icommand:: Execute**會傳回 S_OK，而且狀態為 DB_E_ERRORSOCCURRED。  
  
 OLE DB 核心服務所提供的資料轉換 (**IDataConvert**) 不適用於 DBTYPE_UDT。 不支援其他任何繫結。  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 資料列集的加入和變更  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 原生用戶端加入新的值，或變更到許多核心 OLE DB 結構描述資料列。  
  
#### <a name="the-procedureparameters-schema-rowset"></a>PROCEDURE_PARAMETERS 結構描述資料列集  
 下列是已經針對 PROCEDURE_PARAMETERS 結構描述資料列集所做的加入。  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|三部分名稱的識別碼。|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|三部分名稱的識別碼。|  
|SS_UDT_NAME|DBTYPE_WSTR|三部分名稱的識別碼。|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|組件限定名稱，其中包含類型名稱以及要由 CLR 參考所需的所有組件識別。|  
  
#### <a name="the-sqlassemblies-schema-rowset"></a>SQL_ASSEMBLIES 結構描述資料列集  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開新的提供者特定的結構描述資料列，以描述已註冊的 Udt。 ASSEMBLY 伺服器可指定為 DBTYPE_WSTR，但是不在資料列集內。 如果未指定的話，此資料列集將預設為目前的伺服器。 下表定義了 SQL_ASSEMBLIES 結構描述資料列集。  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|包含該類型之組件的目錄名稱。|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|包含該類型之組件的結構描述名稱或擁有者名稱。 雖然組件是由資料庫指定範圍，而不是由結構描述指定範圍，組件依然有擁有者 (這裡有反映這一點)。|  
|ASSEMBLY_NAME|DBTYPE_WSTR|包含該類型的組件名稱。|  
|ASSEMBLY_ID|DBTYPE_UI4|包含該類型之組件的物件識別碼。|  
|PERMISSION_SET|DBTYPE_WSTR|表示組件之存取範圍的值。 值包括 "SAFE"、"EXTERNAL_ACCESS" 和 "UNSAFE"。|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|組件的二進位表示法。|  
  
#### <a name="the-sqlassemblies-dependencies-schema-rowset"></a>SQL_ASSEMBLIES_ DEPENDENCIES 結構描述資料列集  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開新提供者特有的結構描述資料列集，描述指定之伺服器的組件相依性。 ASSEMBLY_SERVER 可由呼叫端指定為 DBTYPE_WSTR，但是不在資料列集內。 如果未指定的話，此資料列集將預設為目前的伺服器。 下表定義了 SQL_ASSEMBLY_DEPENDENCIES 結構描述資料列集。  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|包含該類型之組件的目錄名稱。|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|包含該類型之組件的結構描述名稱或擁有者名稱。 雖然組件是由資料庫指定範圍，而不是由結構描述指定範圍，組件依然有擁有者 (這裡有反映這一點)。|  
|ASSEMBLY_ID|DBTYPE_UI4|組件的物件識別碼。|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|參考之組件的物件識別碼。|  
  
#### <a name="the-sqlusertypes-schema-rowset"></a>SQL_USER_TYPES 結構描述資料列集  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開新結構描述資料列集 SQL_USER_TYPES，以描述何時加入指定之伺服器的已註冊的 Udt。 UDT_SERVER 必須由呼叫端指定為 DBTYPE_WSTR，但是不在資料列集內。 下表定義了 SQL_USER_TYPES 結構描述資料列集。  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|如果是 UDT 資料行，這個屬性就是指定 UDT 定義所在之目錄名稱的字串。|  
|UDT_SCHEMANAME|DBTYPE_WSTR|如果是 UDT 資料行，這個屬性就是指定 UDT 定義所在之結構描述名稱的字串。|  
|UDT_NAME|DBTYPE_WSTR|包含 UDT 類別的組件名稱。|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|完整類型名稱 (AQN) 包含前面有加上命名空間的類型名稱 (適用的話)。|  
  
#### <a name="the-columns-schema-rowset"></a>COLUMNS 結構描述資料列集  
 COLUMNS 結構描述資料列集的加入項目包含下列資料行。  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|如果是 UDT 資料行，這個屬性就是指定 UDT 定義所在之目錄名稱的字串。|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|如果是 UDT 資料行，這個屬性就是指定 UDT 定義所在之結構描述名稱的字串。|  
|SS_UDT_NAME|DBTYPE_WSTR|UDT 的名稱|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|完整類型名稱 (AQN) 包含前面有加上命名空間的類型名稱 (適用的話)。|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>OLE DB 屬性集的加入和變更  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 原生用戶端加入新的值或變更加入到許多核心 OLE DB 屬性集。  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER 屬性集  
 為了透過 OLE DB 支援 Udt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 會實作新的 DBPROPSET_SQLSERVERPARAMETER 屬性集包含下列值。  
  
|[屬性]|類型|描述|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|三部分名稱的識別碼。<br /><br /> 如果是 UDT 參數，這個屬性就是指定使用者定義型別定義所在之目錄名稱的字串。|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|三部分名稱的識別碼。<br /><br /> 如果是 UDT 參數，這個屬性就是指定使用者定義型別定義所在之結構描述名稱的字串。|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|三部分名稱的識別碼。<br /><br /> 如果是 UDT 資料行，這個屬性就是指定使用者定義型別之單一部分名稱的字串。|  
  
 SSPROP_PARAM_UDT_NAME 為強制性。 SSPROP_PARAM_UDT_CATALOGNAME 和 SSPROP_PARAM_UDT_SCHEMANAME 是選擇性。 如果未正確指定任何屬性，將會傳回 DB_E_ERRORSINCOMMAND。 如果 SSPROP_PARAM_UDT_CATALOGNAME 和 SSPROP_PARAM_UDT_SCHEMANAME 皆未指定，則 UDT 必須定義在與資料表相同的資料庫和結構描述中。 如果 UDT 定義不在與資料表相同的結構描述中 (但是在相同資料庫內)，則必須指定 SSPROP_PARAM_UDT_SCHEMANAME。 如果 UDT 定義位於不同的資料庫內，則必須指定 SSPROP_PARAM_UDT_CATALOGNAME 和 SSPROP_PARAM_UDT_SCHEMANAME 這兩者。  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN 屬性集  
 若要支援中的資料表建立**ITableDefinition**介面，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端會將下列三個新資料行加入到 DBPROPSET_SQLSERVERCOLUMN 屬性集。  
  
|[屬性]|描述|類型|描述|  
|----------|-----------------|----------|-----------------|  
|SSPROP_COL_UDT_CATALOGNAME|UDT_CATALOGNAME|VT_BSTR|如果是 DBTYPE_UDT 類型的資料行，這個屬性就是指定 UDT 定義所在之目錄名稱的字串。|  
|SSPROP_COL_UDT_SCHEMANAME|UDT_SCHEMANAME|VT_BSTR|如果是 DBTYPE_UDT 類型的資料行，這個屬性就是指定 UDT 定義所在之結構描述名稱的字串。|  
|SSPROP_COL_UDT_NAME|UDT_NAME|VT_BSTR|如果是 DBTYPE_UDT 類型的資料行，這個屬性就是指定 UDT 之單一部分名稱的字串。 如果是其他資料行類型，這個屬性會傳回空字串。|  
  
> [!NOTE]  
>  UDT 不會出現在 PROVIDER_TYPES 結構描述資料列集中。 所有資料行都有讀取和寫入存取權。  
  
 ADO 將會使用描述欄中的對應項目來參考這些屬性。  
  
 SSPROP_COL_UDTNAME 是強制性。 SSPROP_COL_UDT_CATALOGNAME 和 SSPROP_COL_UDT_SCHEMANAME 是選擇性。 如果未正確指定任何屬性，將會傳回 `DB_E_ERRORSINCOMMAND`。  
  
 如果 SSPROP_COL_UDT_CATALOGNAME 或 SSPROP_COL_UDT_SCHEMANAME 皆未指定，則 UDT 必須定義在與資料表相同的資料庫和結構描述中。  
  
 如果 UDT 定義不在與資料表相同的結構描述中 (但是在相同資料庫內)，則必須指定 SSPROP_COL_UDT_SCHEMANAME。  
  
 如果 UDT 定義位於不同的資料庫內，則必須指定 SSPROP_COL_UDT_CATALOGNAME 和 SSPROP_COL_UDT_SCHEMANAME 這兩者。  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB 介面的加入和變更  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 原生用戶端加入新的值，或變更到許多核心 OLE DB 介面。  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters 介面  
 若要透過 OLE DB 支援 Udt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 會實作一些變更，包括加入**ISSCommandWithParameters**介面。 這個新介面繼承自核心的 OLE DB 介面**ICommandWithParameters**。 除了繼承自的三種方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，和**SetParameterInfo**;**ISSCommandWithParameters**提供**GetParameterProperties**和**SetParameterProperties**用來處理伺服器特定的方法資料型別。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**介面也可使用新的 ssparamprops 結構。  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset 介面  
 除了**ISSCommandWithParameters**介面，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端也會將新值加入至從呼叫傳回的資料列集**icolumnsrowset:: Getcolumnrowset**方法包括下列項目。  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|UDT 目錄名稱識別碼。|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|UDT 結構描述名稱識別碼。|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|UDT 名稱識別碼。|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|組件限定名稱，其中包含類型名稱以及要由 CLR 參考所需的所有組件識別。|  
  
 當 DBCOLUMN_TYPE 設定為 DBTYPE_UDT 時，您可以查看上面指定的新加入 UDT 中繼資料，讓伺服器 UDT 資料行與二進位類型差異化。 如果該資料有一部分是完整的，伺服器類型會是 UDT。 如果不是 UDT 伺服器類型，這些資料行一定會當做 NULL 傳回。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驅動程式  
 中所做的變更數目[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式為了支援 Udt。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式對應[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]UDT 到 SQL_SS_UDT 驅動程式特有的 SQL 資料類型識別碼。 UDT 資料行顯示為 SQL_SS_UDT。 如果您將對應的 UDT 資料行明確 SQL 陳述式中的另一個型別使用**ToString**或**ToXMLString**方法 UDT 或是透過**CAST/CONVERT**函式、 型別在結果中的資料行集反映出資料行轉換成的實際型別  
  
### <a name="sqlcolattribute-sqldescribeparam-sqlgetdescfield"></a>SQLColAttribute、SQLDescribeParam、SQLGetDescField  
 UDT 資料行的結果集或預存程序/參數化查詢，透過要擷取的 UDT 參數，提供額外的資訊，針對已加入四個新的驅動程式專屬描述項欄位[SQLColAttribute](../../native-client-odbc-api/sqlcolattribute.md)， [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md)，和[SQLGetDescField](../../native-client-odbc-api/sqlgetdescfield.md)函式。  
  
 這四個已經加入的新描述項欄位為 SQL_CA_SS_UDT_CATALOG_NAME、SQL_CA_SS_UDT_SCHEMA_NAME、SQL_CA_SS_UDT_TYPE_NAME 和 SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME。  
  
### <a name="sqlcolumns-sqlprocedurecolumns"></a>SQLColumns、SQLProcedureColumns  
 此外，將三個新的驅動程式特定資料行加入到結果集傳回[SQLColumns](../../native-client-odbc-api/sqlcolumns.md)和[SQLProcedureColumns](../../native-client-odbc-api/sqlprocedurecolumns.md)函數來提供其他資訊有關 UDT 結果資料行或是 UDT 參數設定。 這三個新的資料行為 SS_UDT_CATALOG_NAME、SS_UDT_SCHEMA_NAME 和 SS_UDT_ASSEMBLY_TYPE_NAME。  
  
### <a name="supported-conversions"></a>支援的轉換  
 當從 SQL 轉換成 C 資料類型時，SQL_C_WCHAR、SQL_C_BINARY 和 SQL_C_CHAR 全都可以轉換成 SQL_SS_UDT。 但是請注意，當從 SQL_C_WCHAR 和 SQL_C_CHAR SQL 資料類型轉換時，二進位資料會轉換成十六進位字串。  
  
 當從 C 轉換成 SQL 資料類型時，SQL_C_WCHAR、SQL_C_BINARY 和 SQL_C_CHAR 全都可以轉換成 SQL_SS_UDT。 但是請注意，當從 SQL_C_WCHAR 和 SQL_C_CHAR SQL 資料類型轉換時，二進位資料會轉換成十六進位字串。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  