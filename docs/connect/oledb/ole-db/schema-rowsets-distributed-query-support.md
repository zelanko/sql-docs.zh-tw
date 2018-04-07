---
title: 分散式查詢支援在結構描述資料列 |Microsoft 文件
description: 分散式查詢支援在結構描述資料列集
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], OLE DB Driver for SQL Server
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 26cf4847d1d4f9e6799b2751e81a44e9cc4bcc72
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="schema-rowsets---distributed-query-support"></a>結構描述資料列的分散式的查詢支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  若要支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]分散式查詢中，SQL Server OLE DB 驅動程式**IDBSchemaRowset**介面會傳回連結伺服器上的中繼資料。  
  
 如果 DBPROPSET_SQLSERVERSESSION 屬性 SSPROP_QUOTEDCATALOGNAMES 是 VARIANT_TRUE，您就可以針對目錄名稱指定引號識別碼 (例如 "my.catalog")。 當限制結構描述資料列集輸出目錄，SQL Server OLE DB 驅動程式會辨識包含連結的伺服器和目錄名稱的兩部分名稱。 下表中的結構描述資料列集指定兩部分目錄名稱為*linked_server***。***目錄*將輸出限制為具名連結伺服器的適用目錄。  
  
|結構描述資料列集|目錄限制|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMNS|TABLE_CATALOG|  
|DBSCHEMA_PRIMARY_KEYS|TABLE_CATALOG|  
|DBSCHEMA_TABLES|TABLE_CATALOG|  
|DBSCHEMA_FOREIGN_KEYS|PK_TABLE_CATALOG FK_TABLE_CATALOG|  
|DBSCHEMA_INDEXES|TABLE_CATALOG|  
|DBSCHEMA_COLUMN_PRIVILEGES|TABLE_CATALOG|  
|DBSCHEMA_TABLE_PRIVILEGES|TABLE_CATALOG|  
  
> [!NOTE]  
>  若要限制從連結伺服器的所有目錄結構描述資料列，請使用語法*linked_server* （其中句號分隔符號是名稱規格的一部分）。 這個語法相當於針對目錄名稱限制指定 NULL，而且也會在連結的伺服器指出不支援目錄的資料來源時使用。  
  
 SQL Server OLE DB 驅動程式會定義結構描述資料列集 LINKEDSERVERS，並傳回註冊成連結伺服器的 OLE DB 資料來源的清單。  
  
## <a name="see-also"></a>另請參閱  
 [結構描述資料列集支援&#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 資料列集&#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
