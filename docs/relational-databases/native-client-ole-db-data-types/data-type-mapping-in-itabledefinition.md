---
title: "ITableDefinition 中的資料類型對應 |Microsoft 文件"
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
- SQL Server Native Client OLE DB provider, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
ms.assetid: 13292d1f-c17e-4d11-bf98-3460a10cbb18
caps.latest.revision: "35"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6e67b2b12d10053478013d737df7120c2047f60
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition 中的資料類型對應
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  藉由建立資料表時**itabledefinition:: Createtable**函式， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者可以指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的資料類型*pwszTypeName*傳遞之 DBCOLUMNDESC 陣列的成員。 如果取用者會依名稱指定資料行的資料類型，OLE DB 資料類型對應，由*wType* DBCOLUMNDESC 結構的成員會被忽略。  
  
 使用 DBCOLUMNDESC 結構的 OLE DB 資料類型指定新的資料行資料類型時*wType*成員[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者對應 OLE DB 資料類型，如下所示。  
  
|OLE DB 資料類型|SQL Server<br /><br /> 資料類型|其他資訊|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**二進位**， **varbinary**，**映像，**或**varbinary （max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會檢查*ulColumnSize* DBCOLUMNDESC 結構的成員。 根據值和新版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會對應至型別**映像**。<br /><br /> 如果值*ulColumnSize*小於最大長度**二進位**資料類型資料行，然後在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會檢查 DBCOLUMNDESC *rgPropertySets*成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會對應至型別**二進位**。 如果屬性的值是 VARIANT_FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會對應至型別**varbinary**。 在任一情況，DBCOLUMNDESC *ulColumnSize*成員會決定建立的 SQL Server 資料行的寬度。|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會檢查 DBCOLUMDESC *bPrecision*和*bScale*成員來決定有效位數及縮放的**數值**資料行。|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**， **varchar**，**文字**或**varchar （max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會檢查*ulColumnSize* DBCOLUMNDESC 結構的成員。 根據值和版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會對應至型別**文字**。<br /><br /> 如果值*ulColumnSize*小於多位元組字元資料類型資料行的最大長度則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會檢查 DBCOLUMNDESC *rgPropertySets*成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會對應至型別**char**。 如果屬性的值是 VARIANT_FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會對應至型別**varchar**。 在任一情況，DBCOLUMNDESC *ulColumnSize*成員決定的寬度[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立資料行。|  
|DBTYPE_UDT|**UDT**|下列資訊用於**DBCOLUMNDESC**結構由**itabledefinition:: Createtable**需要 UDT 資料行時：<br /><br /> *pwSzTypeName*會被忽略。<br /><br /> *rgPropertySets*必須包含**DBPROPSET_SQLSERVERCOLUMN**屬性設定為上一節中所述**DBPROPSET_SQLSERVERCOLUMN**，請在[使用使用者定義型別](../../relational-databases/native-client/features/using-user-defined-types.md)。|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**， **nvarchar**， **ntext**或**nvarchar （max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會檢查*ulColumnSize* DBCOLUMNDESC 結構的成員。 根據值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會對應至型別**ntext**。<br /><br /> 如果值*ulColumnSize*小於 Unicode 字元資料類型資料行的最大長度則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會檢查 DBCOLUMNDESC *rgPropertySets*成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會對應至型別**nchar**。 如果屬性的值是 VARIANT_FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會對應至型別**nvarchar**。 在任一情況，DBCOLUMNDESC *ulColumnSize*成員決定的寬度[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立資料行。|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  建立新的資料表時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者只會對應上表中指定的 OLE DB 資料類型列舉值。 嘗試建立含有任何其他 OLE DB 資料類型之資料行的資料表都會產生錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
