---
title: ITableDefinition 中的資料類型對應 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e561742406c173b69bfb5040c2f2f51efdf5ed64
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63201221"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition 中的資料類型對應
  使用**ITableDefinition：： CreateTable**函數來建立資料表時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者可以在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳遞之 DBCOLUMNDESC 陣列的*pwszTypeName*成員中指定資料類型。 如果取用者依照名稱來指定資料行的資料類型，系統就會忽略 OLE DB 資料對應 (由 DBCOLUMNDESC 結構的 *wType* 成員代表)。  
  
 使用 DBCOLUMNDESC 結構*wType*成員來指定具有 OLE DB 資料類型的新資料行資料類型時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，Native Client OLE DB 提供者會對應 OLE DB 的資料類型，如下所示。  
  
|OLE DB 資料類型|SQL Server<br /><br /> 資料類型|其他資訊|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**、**varbinary**、**image** 或 **varbinary(max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會檢查 DBCOLUMNDESC 結構的*ulColumnSize*成員。 根據[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例的值和版本， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會將此類型對應至**影像**。<br /><br /> 如果*ulColumnSize*的值小於**binary**資料類型資料行的最大長度，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT OLE DB 提供者會檢查 DBCOLUMNDESC *rgPropertySets*成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者就會將此類型對應至**binary**。 如果屬性的值是 VARIANT_FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者就會將此類型對應至**Varbinary**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 SQL Server 資料行的寬度。|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|Native Client OLE DB 提供者會檢查 DBCOLUMDESC *bPrecision*和*bScale*成員，以判斷數值資料行的有效位數和小數位數。 **numeric** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**、**varchar**、**text** 或 **varchar(max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會檢查 DBCOLUMNDESC 結構的*ulColumnSize*成員。 根據[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例的值和版本， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會將此類型對應至**文字**。<br /><br /> 如果*ulColumnSize*的值小於多位元組字元資料類型資料行的最大長度，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會檢查 DBCOLUMNDESC *rgPropertySets*成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者就會將此類型對應至**char**。 如果屬性的值是 VARIANT_FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者就會將此類型對應到**Varchar**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料行的寬度。|  
|DBTYPE_UDT|**UDT**|當需要 UDT 資料行時`DBCOLUMNDESC` ，下列資訊會在**ITableDefinition：： CreateTable**結構中使用：<br /><br /> -   已忽略*pwSzTypeName* 。<br />-   *rgPropertySets*必須包含`DBPROPSET_SQLSERVERCOLUMN`屬性集`DBPROPSET_SQLSERVERCOLUMN`，如[使用使用者定義類型](../native-client/features/using-user-defined-types.md)中的一節中所述。|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**、**nvarchar**、**ntext** 或 **nvarchar(max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會檢查 DBCOLUMNDESC 結構的*ulColumnSize*成員。 根據值， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會將此類型對應至**Ntext**。<br /><br /> 如果*ulColumnSize*的值小於 Unicode 字元資料類型資料行的最大長度，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會檢查 DBCOLUMNDESC *rgPropertySets*成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者就會將此類型對應到**Nchar**。 如果屬性的值是 VARIANT_FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者就會將此類型對應至**Nvarchar**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料行的寬度。|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  建立新的資料表時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者只會對應上表中指定的 OLE DB 資料類型列舉值。 嘗試建立含有任何其他 OLE DB 資料類型之資料行的資料表都會產生錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;OLE DB&#41;](data-types-ole-db.md)  
  
  
