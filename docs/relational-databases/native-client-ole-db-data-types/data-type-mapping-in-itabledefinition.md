---
title: ITableDefinition 中的資料類型對應 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3e828efa513db1ace272e59379f77d063220290
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297020"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition 中的資料類型對應
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  使用**ITable 定義:建立表**函數建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表時, 本機用戶端 OLE[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB 提供程式使用者可以在 傳遞的 DBCOLUMNDESC 陣列的*pwszTypeName*成員中指定資料類型。 如果取用者依照名稱來指定資料行的資料類型，系統就會忽略 OLE DB 資料對應 (由 DBCOLUMNDESC 結構的 *wType* 成員代表)。  
  
 使用 DBCOLUMN DB 資料類型使用 DBCOLUMN DB[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構*wType*成員指定新的列數據類型時,本機用戶端 OLE DB 提供程式將 OLE DB 資料類型映射如下。  
  
|OLE DB 資料類型|SQL Server<br /><br /> 資料類型|其他資訊|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**、**varbinary**、**image** 或 **varbinary(max)**|本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式檢查 DBCOLUMNDESC 結構的*ulColumnSize*成員。 從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實體的值與版本,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]這個機客戶端 OLE DB 提供軟體會對映射到**映像**。<br /><br /> 如果*ulColumnSize*的值小於**二進位**資料類型列的最大長[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]度,則本機用戶端 OLE DB 提供程式將檢查 DBCOLUMNDESC *rgPropertySet*成員。 如果DBPROP_COL_FIXEDLENGTHVARIANT_TRUE,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 OLE DB 提供應用程式將類型映射到**二進位**。 如果屬性的值VARIANT_FALSE,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 OLE DB 提供程式將類型映射到**varbinary**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 SQL Server 資料行的寬度。|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**UNIQUEIDENTIFIER**||  
|DBTYPE_I2|**小林特**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**公尺**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式檢查 DBCOLUMDESC *bPrecision*和*bScale*成員,以確定**數位**列的精度和比例。|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**浮動**||  
|DBTYPE_STR|**char**、**varchar**、**text** 或 **varchar(max)**|本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式檢查 DBCOLUMNDESC 結構的*ulColumnSize*成員。 從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實體的值與版本,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]這個機客戶端 OLE DB 提供軟體會對**文字**。<br /><br /> 如果*ulColumnSize*的值小於多位元組位元數據類型列的最大長[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]度,則 本機用戶端 OLE 資料庫提供程式將檢查 DBCOLUMNDESC *rgPropertySet*成員。 如果DBPROP_COL_FIXEDLENGTHVARIANT_TRUE,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 OLE DB 提供程式將類型映射到**字元**。 如果屬性的值為VARIANT_FALSE,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 OLE DB 提供程式將類型映射到**varchar**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料行的寬度。|  
|DBTYPE_UDT|**Udt**|當需要 UDT 資料行時，下列資訊會用於 **ITableDefinition::CreateTable** 所使用的 **DBCOLUMNDESC** 結構中：<br /><br /> 已忽略 *pwSzTypeName*。<br /><br /> *rgPropertySets* 必須包含 **DBPROPSET_SQLSERVERCOLUMN** 屬性集，如[使用使用者定義型別](../../relational-databases/native-client/features/using-user-defined-types.md)中有關 **DBPROPSET_SQLSERVERCOLUMN** 的小節中所述。|  
|DBTYPE_UI1|**小金特**||  
|DBTYPE_WSTR|**nchar**、**nvarchar**、**ntext** 或 **nvarchar(max)**|本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式檢查 DBCOLUMNDESC 結構的*ulColumnSize*成員。 基於該值,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 OLE DB 提供程式將類型映射到**ntext**。<br /><br /> 如果*ulColumnSize*的值小於 Unicode 字元數據類型列的最大[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]長度,則 本機用戶端 OLE 資料庫提供程式將檢查 DBCOLUMNDESC *rgPropertySet*成員。 如果VARIANT_TRUEDBPROP_COL_FIXEDLENGTH,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 OLE DB 提供程式將類型映射到**nchar**。 如果屬性的值VARIANT_FALSE,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 OLE DB 提供程式將類型映射到**nvarchar**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料行的寬度。|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  建立新的資料表時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者只會對應上表中指定的 OLE DB 資料類型列舉值。 嘗試建立含有任何其他 OLE DB 資料類型之資料行的資料表都會產生錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
