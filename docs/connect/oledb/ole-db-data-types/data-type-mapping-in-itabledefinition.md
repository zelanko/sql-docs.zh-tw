---
title: ITableDefinition 中的資料類型對應 |Microsoft Docs
description: ITableDefinition 中的資料類型對應
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
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 5dcd4b33121d5459120572b2b31de413106aeeda
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66775596"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition 中的資料類型對應
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  使用 **ITableDefinition::CreateTable** 函數來建立資料表時，OLE DB Driver for SQL Server 取用者可以在傳遞之 DBCOLUMNDESC 陣列的 *pwszTypeName* 成員中指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。 如果取用者依照名稱來指定資料行的資料類型，系統就會忽略 OLE DB 資料對應 (由 DBCOLUMNDESC 結構的 *wType* 成員代表)。  
  
 使用 DBCOLUMNDESC 結構 *wType* 成員來指定具有 OLE DB 資料類型的新資料行資料類型時，OLE DB Driver for SQL Server 會依照下列方式對應 OLE DB 資料類型。  
  
|OLE DB 資料類型|SQL Server<br /><br /> 資料類型|其他資訊|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**、**varbinary**、**image** 或 **varbinary(max)**|OLE DB Driver for SQL Server 會檢查*ulColumnSize* DBCOLUMNDESC 結構的成員。 根據值和新版[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體，OLE DB Driver for SQL Server 將對應的型別**映像**。<br /><br /> 如果 *ulColumnSize* 的值小於 **binary** 資料類型資料行的最大長度，OLE DB Driver for SQL Server 就會檢查 DBCOLUMNDESC *rgPropertySets* 成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，OLE DB Driver for SQL Server 會將對應的型別**二進位**。 如果屬性的值是 VARIANT_FALSE，OLE DB Driver for SQL Server 會將對應的型別**varbinary**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 SQL Server 資料行的寬度。|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|OLE DB Driver for SQL Server 會檢查 DBCOLUMDESC *bPrecision* 和 *bScale* 成員來決定 **numeric** 資料行的有效位數和小數位數。|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**、**varchar**、**text** 或 **varchar(max)**|OLE DB Driver for SQL Server 會檢查*ulColumnSize* DBCOLUMNDESC 結構的成員。 根據值和新版[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體，OLE DB Driver for SQL Server 將對應的型別**文字**。<br /><br /> 如果 *ulColumnSize* 的值小於多位元組字元資料類型資料行的最大長度，OLE DB Driver for SQL Server 就會檢查 DBCOLUMNDESC *rgPropertySets* 成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，OLE DB Driver for SQL Server 會將對應的型別**char**。 如果屬性的值是 VARIANT_FALSE，OLE DB Driver for SQL Server 會將對應的型別**varchar**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料行的寬度。|  
|DBTYPE_UDT|**UDT**|當需要 UDT 資料行時，下列資訊會用於 **ITableDefinition::CreateTable** 所使用的 **DBCOLUMNDESC** 結構中：<br /><br /> *pwSzTypeName*會被忽略。<br /><br /> *rgPropertySets*必須包含**DBPROPSET_SQLSERVERCOLUMN**屬性設定為上一節中所述**DBPROPSET_SQLSERVERCOLUMN**中[Using User-Defined 類型](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|**nchar**、**nvarchar**、**ntext** 或 **nvarchar(max)**|OLE DB Driver for SQL Server 會檢查*ulColumnSize* DBCOLUMNDESC 結構的成員。 根據值，OLE DB Driver for SQL Server 將此類型對應至**ntext**。<br /><br /> 如果 *ulColumnSize* 的值小於 Unicode 字元資料類型資料行的最大長度，OLE DB Driver for SQL Server 就會檢查 DBCOLUMNDESC *rgPropertySets* 成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，OLE DB Driver for SQL Server 會將對應的型別**nchar**。 如果屬性的值是 VARIANT_FALSE，OLE DB Driver for SQL Server 會將對應的型別**nvarchar**。 不論是哪一種情況，DBCOLUMNDESC *ulColumnSize* 成員都會決定所建立之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料行的寬度。|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  建立新的資料表時，OLE DB Driver for SQL Server 只會對應上表中指定的 OLE DB 資料類型列舉值。 嘗試建立含有任何其他 OLE DB 資料類型之資料行的資料表都會產生錯誤。  

## <a name="see-also"></a>另請參閱  
 [資料型別&#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
