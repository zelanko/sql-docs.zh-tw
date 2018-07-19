---
title: ITableDefinition 中的資料類型對應 |Microsoft 文件
description: ITableDefinition 中的資料類型對應
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d613fc7be394bbf16c86c5e217e3dfe83a4296a1
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2018
ms.locfileid: "35666348"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition 中的資料類型對應
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  藉由建立資料表時**itabledefinition:: Createtable**函式，可以指定 SQL Server 取用者，OLE DB 驅動程式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的資料類型*pwszTypeName*的成員為傳遞之 DBCOLUMNDESC 陣列。 如果取用者會依名稱指定資料行的資料類型，OLE DB 資料類型對應，由*wType* DBCOLUMNDESC 結構的成員會被忽略。  
  
 使用 DBCOLUMNDESC 結構的 OLE DB 資料類型指定新的資料行資料類型時*wType*成員，SQL Server OLE DB 驅動程式就會對應 OLE DB 資料類型，如下所示。  
  
|OLE DB 資料類型|[SQL Server]<br /><br /> 資料類型|其他資訊|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**二進位**， **varbinary**，**映像，** 或**varbinary （max)**|SQL Server OLE DB 驅動程式會檢查*ulColumnSize* DBCOLUMNDESC 結構的成員。 根據值和新版[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體，OLE DB 驅動程式的 SQL Server 將對應的型別**映像**。<br /><br /> 如果值*ulColumnSize*小於最大長度**二進位**資料類型資料行，則 SQL Server OLE DB 驅動程式會檢查 DBCOLUMNDESC *rgPropertySets*成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，SQL Server OLE DB 驅動程式會將對應的型別**二進位**。 如果屬性的值是 VARIANT_FALSE，SQL Server OLE DB 驅動程式會對應至型別**varbinary**。 在任一情況，DBCOLUMNDESC *ulColumnSize*成員會決定建立的 SQL Server 資料行的寬度。|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|SQL Server OLE DB 驅動程式會檢查 DBCOLUMDESC *bPrecision*和*bScale*成員來決定有效位數及縮放的**數值**資料行。|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**， **varchar**，**文字**或**varchar （max)**|SQL Server OLE DB 驅動程式會檢查*ulColumnSize* DBCOLUMNDESC 結構的成員。 根據值和版本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體，OLE DB 驅動程式的 SQL Server 將對應的型別**文字**。<br /><br /> 如果值*ulColumnSize*小於多位元組字元資料類型資料行，則 OLE DB 驅動程式的最大長度為 SQL Server 就會檢查 DBCOLUMNDESC *rgPropertySets*成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，SQL Server OLE DB 驅動程式會將對應的型別**char**。 如果屬性的值是 VARIANT_FALSE，SQL Server OLE DB 驅動程式會對應至型別**varchar**。 在任一情況，DBCOLUMNDESC *ulColumnSize*成員決定的寬度[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]建立資料行。|  
|DBTYPE_UDT|**UDT**|下列資訊用於**DBCOLUMNDESC**結構由**itabledefinition:: Createtable**需要 UDT 資料行時：<br /><br /> *pwSzTypeName*會被忽略。<br /><br /> *rgPropertySets*必須包含**DBPROPSET_SQLSERVERCOLUMN**屬性設定為上一節中所述**DBPROPSET_SQLSERVERCOLUMN**，請在[Using User-Defined 類型](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|**nchar**， **nvarchar**， **ntext**或**nvarchar （max)**|SQL Server OLE DB 驅動程式會檢查*ulColumnSize* DBCOLUMNDESC 結構的成員。 根據值，SQL Server OLE DB 驅動程式將此類型對應至**ntext**。<br /><br /> 如果值*ulColumnSize*小於 Unicode 字元資料類型資料行，則 OLE DB 驅動程式的最大長度為 SQL Server 就會檢查 DBCOLUMNDESC *rgPropertySets*成員。 如果 DBPROP_COL_FIXEDLENGTH 是 VARIANT_TRUE，SQL Server OLE DB 驅動程式會將對應的型別**nchar**。 如果屬性的值是 VARIANT_FALSE，SQL Server OLE DB 驅動程式會對應至型別**nvarchar**。 在任一情況，DBCOLUMNDESC *ulColumnSize*成員決定的寬度[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]建立資料行。|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  當建立新的資料表，SQL Server OLE DB 驅動程式對應只 OLE DB 資料類型列舉值指定在上表中。 嘗試建立含有任何其他 OLE DB 資料類型之資料行的資料表都會產生錯誤。  

## <a name="see-also"></a>另請參閱  
 [資料型別&#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
