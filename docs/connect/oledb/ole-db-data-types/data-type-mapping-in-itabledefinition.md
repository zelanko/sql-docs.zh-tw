---
title: ITableDefinition 中的資料類型對應 (OLE DB driver) | Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 取用者如何使用 ITableDefinition::CreateTable 方法，在建立資料表時指定 SQL Server 資料類型。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- OLE DB Driver for SQL Server, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fecca9ed46ea35fe45868b8c618b3514f0b04abd
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860120"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition 中的資料類型對應
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  使用 **ITableDefinition::CreateTable** 函數來建立資料表時，OLE DB Driver for SQL Server 取用者可以在傳遞之 DBCOLUMNDESC 陣列的 *pwszTypeName* 成員中指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。 如果取用者依照名稱來指定資料行的資料類型，系統就會忽略 OLE DB 資料對應 (由 DBCOLUMNDESC 結構的 *wType* 成員代表)。  
  
 使用 DBCOLUMNDESC 結構 *wType* 成員來指定具有 OLE DB 資料類型的新資料行資料類型時，OLE DB Driver for SQL Server 會依照下列方式對應 OLE DB 資料類型。  
  
|OLE DB 資料類型|SQL Server<br /><br /> 資料類型|其他資訊|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**、**varbinary**、**image** 或 **varbinary(max)**|OLE DB Driver for SQL Server 會檢查 DBCOLUMNDESC 結構的 *ulColumnSize* 成員。 OLE DB Driver for SQL Server 會根據此值以及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的版本，將此類型對應至 **image**。<br /><br /> 如果 *ulColumnSize* 的值小於 **binary** 資料類型資料行的最大長度，OLE DB Driver for SQL Server 就會檢查 DBCOLUMNDESC *rgPropertySets* 成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，OLE DB Driver for SQL Server 就會將此類型對應至 **binary**。 如果屬性的值是 VARIANT_FALSE，OLE DB Driver for SQL Server 就會將此類型對應至 **varbinary**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 SQL Server 資料行的寬度。|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|OLE DB Driver for SQL Server 會檢查 DBCOLUMDESC *bPrecision* 和 *bScale* 成員來決定 **numeric** 資料行的有效位數和小數位數。|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**、**varchar**、**text** 或 **varchar(max)**|OLE DB Driver for SQL Server 會檢查 DBCOLUMNDESC 結構的 *ulColumnSize* 成員。 OLE DB Driver for SQL Server 會根據此值以及 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的版本，將此類型對應至 **text**。<br /><br /> 如果 *ulColumnSize* 的值小於多位元組字元資料類型資料行的最大長度，OLE DB Driver for SQL Server 就會檢查 DBCOLUMNDESC *rgPropertySets* 成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，OLE DB Driver for SQL Server 就會將此類型對應至 **char**。 如果屬性的值是 VARIANT_FALSE，OLE DB Driver for SQL Server 就會將此類型對應至 **varchar**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料行的寬度。|  
|DBTYPE_UDT|**UDT**|當需要 UDT 資料行時，下列資訊會用於 **ITableDefinition::CreateTable** 所使用的 **DBCOLUMNDESC** 結構中：<br /><br /> 已忽略 *pwSzTypeName*。<br /><br /> *rgPropertySets* 必須包含 **DBPROPSET_SQLSERVERCOLUMN** 屬性集，如[使用使用者定義型別](../../oledb/features/using-user-defined-types.md)中有關 **DBPROPSET_SQLSERVERCOLUMN** 的小節中所述。|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|**nchar**、**nvarchar**、**ntext** 或 **nvarchar(max)**|OLE DB Driver for SQL Server 會檢查 DBCOLUMNDESC 結構的 *ulColumnSize* 成員。 OLE DB Driver for SQL Server 會根據此值，將此類型對應至 **ntext**。<br /><br /> 如果 *ulColumnSize* 的值小於 Unicode 字元資料類型資料行的最大長度，OLE DB Driver for SQL Server 就會檢查 DBCOLUMNDESC *rgPropertySets* 成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，OLE DB Driver for SQL Server 就會將此類型對應至 **nchar**。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，OLE DB Driver for SQL Server 就會將此類型對應至 **nvarchar**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料行的寬度。|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  建立新的資料表時，OLE DB Driver for SQL Server 只會對應上表中指定的 OLE DB 資料類型列舉值。 嘗試建立含有任何其他 OLE DB 資料類型之資料行的資料表都會產生錯誤。  

## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
