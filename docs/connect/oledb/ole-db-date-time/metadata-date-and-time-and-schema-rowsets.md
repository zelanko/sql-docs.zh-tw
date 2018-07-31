---
title: 日期和時間以及結構描述資料列 |Microsoft Docs
description: 日期和時間以及結構描述資料列集
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e2e1192cb0f69f72075a9e6164b91def61c80871
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109650"
---
# <a name="metadata---date-and-time-and-schema-rowsets"></a>中繼資料 - 日期和時間以及結構描述資料列集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本主題提供有關 COLUMNS 資料列集和 PROCEDURE_PARAMETERS 資料列集的資訊。 這項資訊與 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中引進的 OLE DB 日期和時間增強功能相關。  
  
## <a name="columns-rowset"></a>COLUMNS 資料列集  
 系統會傳回日期/時間類型的下列資料行值：  
  
|資料行類型|DATA_TYPE|COLUMN_FLAGS、DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|日期|DBTYPE_DBDATE|Clear|0|  
|time|DBTYPE_DBTIME2|將|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|Clear|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|Clear|3|  
|datetime2|DBTYPE_DBTIMESTAMP|將|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|將|0..7|  
  
 在 COLUMN_FLAGS 中，DBCOLUMNFLAGS_ISFIXEDLENGTH 對 date/time 類型永遠為 true，而且下列旗標永遠為 false：  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 剩餘的旗標 (DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE 和 DBCOLUMNFLAGS_WRITEUNKNOWN) 可以根據資料行的定義方式來設定。  
  
 在 COLUMN_FLAGS 中會提供新旗標 DBCOLUMNFLAGS_SS_ISVARIABLESCALE，以允許應用程式判斷資料行的伺服器類型，其中 DATA_TYPE 是 DBTYPE_DBTIMESTAMP。 DATETIME_PRECISION 也必須用來識別伺服器類型。  
  
 只有連接到 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 或更新版本的伺服器時，DBCOLUMNFLAGS_SS_ISVARIABLESCALE 才有效。 連接到下層伺服器時，不會定義 DBCOLUMNFLAGS_SS_ISFIXEDSCALE。  
  
## <a name="procedureparameters-rowset"></a>PROCEDURE_PARAMETERS 資料列集  
 DATA_TYPE 包含與 COLUMNS 結構描述資料列集相同的值，而 TYPE_NAME 包含伺服器類型。  
  
 已經加入新的資料行 SS_DATETIME_PRECISION，以傳回與 DATETIME_PRECISION 資料行相同的類型，類似 COLUMNS 資料列集。  
  
## <a name="providertypes-rowset"></a>PROVIDER_TYPES 資料列集  
 系統會傳回日期/時間類型的下列資料列：  
  
|類型 -><br /><br /> 「資料行」|日期|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|日期|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|scale|NULL|NULL|scale|scale|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|日期|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|除非下列其中之一是 true，否則為 VARIANT_TRUE：<br /><br /> 這是連接到下層伺服器的用戶端。<br /><br /> 資料類型相容性連接屬性會指定等於 80 的相容性層級。|除非下列其中之一是 true，否則為 VARIANT_TRUE：<br /><br /> 這是連接到下層伺服器的用戶端。<br /><br /> 資料類型相容性連接屬性會指定等於 80 的相容性層級。|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 OLE DB 只會定義數值和十進位類型的 MINIMUM_SCALE 和 MAXIMUM_SCALE，因此 OLE DB Driver for SQL Server 對於 time、datetime2 和 datetimeoffset 這些資料行的用法不是標準的。  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料&#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
  
  
