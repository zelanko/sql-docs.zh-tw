---
title: "資料列集和參數中的資料類型對應 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-data-types
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- DBTYPE_SQLVARIANT data type
- SQL Server Native Client OLE DB provider, data types
- rowsets [OLE DB], data type mapping
- data types [OLE DB]
- GetColumnInfo function
- parameters [OLE DB]
- SSPROP_ALLOWNATIVEVARIANT property
- GetParameterInfo function
- OLE DB, data types
ms.assetid: 3d831ff8-3b79-4698-b2c1-2b5dd2f8235c
caps.latest.revision: "41"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 721f1891aefadf29070fdaf714c449bebb806ee7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="data-type-mapping-in-rowsets-and-parameters"></a>資料列集和參數中的資料類型對應
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在資料列集，做為參數值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者代表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料使用下列的 OLE DB 定義的資料類型，函數中報告**icolumnsinfo:: Getcolumninfo**和**Icommandwithparameters:: Getparameterinfo**。  
  
|SQL Server 資料類型|OLE DB 資料類型|  
|--------------------------|----------------------|  
|**bigint**|DBTYPE_I8|  
|**binary**|DBTYPE_BYTES|  
|**bit**|DBTYPE_BOOL|  
|**char**|DBTYPE_STR|  
|**datetime**|DBTYPE_DBTIMESTAMP|  
|**datetime2**|DBTYPE_DBTIME2|  
|**decimal**|DBTYPE_NUMERIC|  
|**float**|DBTYPE_R8|  
|**image**|DBTYPE_BYTES|  
|**int**|DBTYPE_I4|  
|**money**|DBTYPE_CY|  
|**nchar**|DBTYPE_WSTR|  
|**ntext**|DBTYPE_WSTR|  
|**numeric**|DBTYPE_NUMERIC|  
|**nvarchar**|DBTYPE_WSTR|  
|**real**|DBTYPE_R4|  
|**smalldatetime**|DBTYPE_DBTIMESTAMP|  
|**smallint**|DBTYPE_I2|  
|**smallmoney**|DBTYPE_CY|  
|**sql_variant**|DBTYPE_VARIANT、DBTYPE_SQLVARIANT|  
|**sysname**|DBTYPE_WSTR|  
|**text**|DBTYPE_STR|  
|**timestamp**|DBTYPE_BYTES|  
|**tinyint**|DBTYPE_UI1|  
|**UDT**|DBTYPE_UDT|  
|**uniqueidentifier**|DBTYPE_GUID|  
|**varbinary**|DBTYPE_BYTES|  
|**varchar**|DBTYPE_STR|  
|**XML**|DBTYPE_XML|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援取用者要求資料轉換，如下圖所示。  
  
 **Sql_variant**物件可以保存的任何資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除了 text、 ntext、 image、 varchar （max）、 nvarchar （max）、 varbinary （max）、 xml、 時間戳記和 Microsoft.NET Framework common language runtime (CLR) 類型的資料使用者定義型別。 sql_variant 資料的執行個體不能用 sql_variant 做為它的基礎基底資料類型。 例如，資料行可以包含**smallint**某些資料列的值**float**其他資料列，值和**char**/**nchar**其餘部分中的值。  
  
> [!NOTE]  
>  **Sql_variant**資料類型會類似於在 Microsoft Visual Basic® 和 DBTYPE_VARIANT、 DBTYPE_SQLVARIANT OLEDB 中的 Variant 資料類型。  
  
 當**sql_variant**資料以 DBTYPE_VARIANT 提取，它會放在緩衝區中的 VARIANT 結構。 但是 VARIANT 結構中的子類型可能不會對應到定義於**sql_variant**資料型別。 **Sql_variant**資料必須再擷取以 DBTYPE_SQLVARIANT 為了讓要比對所有的子類型。  
  
## <a name="dbtypesqlvariant-data-type"></a>DBTYPE_SQLVARIANT 資料類型  
 若要支援**sql_variant**資料型別， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開稱為 DBTYPE_SQLVARIANT 的提供者特定資料類型。 當**sql_variant**資料以 DBTYPE_SQLVARIANT 提取中，它會儲存在提供者特定的 SSVARIANT 結構。 SSVARIANT 結構包含所有符合的子類型的子**sql_variant**資料型別。  
  
 工作階段屬性 SSPROP_ALLOWNATIVEVARIANT 也必須設定為 TRUE。  
  
## <a name="provider-specific-property-sspropallownativevariant"></a>提供者特定的屬性 SSPROP_ALLOWNATIVEVARIANT  
 您在提取資料時，可以明確地指定要針對資料行或參數傳回何種資料類型。 **IColumnsInfo**也可用來取得資料行資訊，然後使用它來進行繫結。 當**IColumnsInfo**可用來取得用於繫結用途的資料行資訊如果 SSPROP_ALLOWNATIVEVARIANT 工作階段屬性為 FALSE （預設值），就會傳回 DBTYPE_VARIANT **sql_variant**資料行。 如果 SSPROP_ALLOWNATIVEVARIANT 屬性為 FALSE，則 DBTYPE_SQLVARIANT 不受支援。 如果 SSPROP_ALLOWNATIVEVARIANT 屬性設定為 TRUE，則資料行類型會傳回為 DBTYPE_SQLVARIANT，在此種情況下，緩衝區會保存 SSVARIANT 結構。 在提取**sql_variant**資料以 DBTYPE_SQLVARIANT，工作階段屬性 SSPROP_ALLOWNATIVEVARIANT 必須設定為 TRUE。  
  
 SSPROP_ALLOWNATIVEVARIANT 屬性是提供者特定之 DBPROPSET_SQLSERVERSESSION 屬性集的一部分，而且是工作階段屬性。  
  
 DBTYPE_VARIANT 適用於所有其他的 OLE DB 提供者。  
  
## <a name="sspropallownativevariant"></a>SSPROP_ALLOWNATIVEVARIANT  
 SSPROP_ALLOWNATIVEVARIANT 是工作階段屬性，而且是 DBPROPSET_SQLSERVERSESSION 屬性集的一部分。  
  
|||  
|-|-|  
|SSPROP_ALLOWNATIVEVARIANT|類型：VT_BOOL<br /><br /> R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：決定所提取的資料是否為 DBTYPE_VARIANT 或 DBTYPE_SQLVARIANT。<br /><br /> VARIANT_TRUE：資料行類型是以 DBTYPE_SQLVARIANT 傳回，在此種情況下，緩衝區會保存 SSVARIANT 結構。<br /><br /> VARIANT_FALSE：資料行類型是以 DBTYPE_VARIANT 傳回，而且緩衝區將具有 VARIANT 結構。|  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
