---
title: 結構描述資料列集支援 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- SQL Server Native Client OLE DB provider, schema rowsets
- rowsets [OLE DB], schema
ms.assetid: a75b4b69-b095-4690-9b31-a2b32a67489e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e54a81cf47804e1cf4568e739bb2c4cf83b9fe25
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288558"
---
# <a name="schema-rowset-support-ole-db"></a>結構描述資料列集支援 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本機[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供者還[!INCLUDE[tsql](../../../includes/tsql-md.md)]支援在處理 分散式查詢時從連結伺服器返回架構資訊。  
  
> [!NOTE]  
>  雖然 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援同義字，但是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不會傳回同義字的中繼資料。  
  
 下表列出了[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]架構列集和本機用戶端 OLE 資料庫提供程式支援的限制列。  
  
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
 [結構描述資料列集中的分散式查詢支援](../../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md)  
  
 [LINKEDSERVERS 資料列集 &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL 伺服器本機用戶端&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用使用者定義型別](../../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
