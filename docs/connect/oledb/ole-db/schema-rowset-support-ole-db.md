---
title: 結構描述資料列集支援 (OLE DB) | Microsoft Docs
description: 結構描述資料列集支援 (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- OLE DB Driver for SQL Server, schema rowsets
- rowsets [OLE DB], schema
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4734255bc71b7f658b15db5c615910fbf3c6f5a7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993919"
---
# <a name="schema-rowset-support-ole-db"></a>結構描述資料列集支援 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  處理 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 分散式查詢時，OLE DB Driver for SQL Server 也支援從連結伺服器傳回結構描述資訊。  
  
> [!NOTE]  
>  雖然 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援同義字，但是 OLE DB Driver for SQL Server 不會傳回同義字的中繼資料。  
  
 下表列出 OLE DB Driver for SQL Server 所支援的結構描述資料列集與限制資料行。  
  
|結構描述資料列集|限制資料行|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMN_PRIVILEGES|支援所有的限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|DBSCHEMA_COLUMNS|支援所有的限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME<br /><br /> 下列其他的資料行為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 專屬的：<br /><br /> COLUMN_LCID，這是定序的地區設定識別碼。 COLUMN_LCID 與 Windows LCID 的值相同。<br /><br /> COLUMN_COMPFLAGS 會定義定序所支援的比較。 資料格式和 DBPROB_FINDCOMPAREOPS 相同。<br /><br /> COLUMN_SORTID，這是定序的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 排序樣式。<br /><br /> COLUMN_TDSCOLLATION，這是資料行的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 定序。<br /><br /> IS_COMPUTED，如果資料行為計算資料行，這是 VARIANT_TRUE，否則為 VARIANT_FALSE。|  
|DBSCHEMA_FOREIGN_KEYS|支援所有的限制。<br /><br /> PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|DBSCHEMA_INDEXES|支援限制 1、2、3 及 5。<br /><br /> TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TABLE_NAME|  
|DBSCHEMA_PRIMARY_KEYS|支援所有的限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_PROCEDURE_PARAMETERS|支援所有的限制。<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|DBSCHEMA_PROCEDURES|支援限制 1、2 及 3。<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME<br /><br /> DBSCHEMA_PROCEDURES 只會傳回目前使用者可以執行的程序，或是目前使用者已被授與 VIEW DEFINITION 權限的程序。|  
|DBSCHEMA_PROVIDER_TYPES|支援所有的限制。<br /><br /> DATA_TYPE BEST_MATCH|  
|DBSCHEMA_SCHEMATA|支援所有的限制。<br /><br /> CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|DBSCHEMA_STATISTICS|支援所有的限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_TABLE_CONSTRAINTS|支援所有的限制。<br /><br /> CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|DBSCHEMA_TABLE_PRIVILEGES|支援所有的限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|DBSCHEMA_TABLES|支援所有的限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|DBSCHEMA_TABLES_INFO|支援所有的限制。<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
  
## <a name="in-this-section"></a>本節內容  
 [結構描述資料列集中的分散式查詢支援](../../oledb/ole-db/schema-rowsets-distributed-query-support.md)  
  
 [LINKEDSERVERS 資料列集 &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 程式設計](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [使用使用者定義型別](../../oledb/features/using-user-defined-types.md)  
  
  
