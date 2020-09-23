---
title: 結構描述資料列集中的分散式查詢支援 | Microsoft Docs
description: OLE DB Driver for SQL Server 的 IDBSchemaRowset 介面會傳回關於連結的伺服器的中繼資料，以支援 SQL Server 分散式查詢。
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], OLE DB Driver for SQL Server
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61105b2e974cd111cd4f5dfd10e7f528cd04519a
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861560"
---
# <a name="schema-rowsets---distributed-query-support"></a>結構描述資料列集 - 分散式查詢支援
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  為了支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分散式查詢，OLE DB Driver for SQL Server 的 **IDBSchemaRowset** 介面會針對連結的伺服器傳回中繼資料。  
  
 如果 DBPROPSET_SQLSERVERSESSION 屬性 SSPROP_QUOTEDCATALOGNAMES 是 VARIANT_TRUE，您就可以針對目錄名稱指定引號識別碼 (例如 "my.catalog")。 依照目錄來限制結構描述資料列集輸出時，OLE DB Driver for SQL Server 會辨識包含連結伺服器和目錄名稱的兩部分名稱。 針對下表中的結構描述資料列集，將兩部分目錄名稱指定為 _linked\_server_ **.** _catalog_ 就會將輸出限制為具名連結伺服器的適用目錄。  
  
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
>  若要將結構描述資料列集限制為連結伺服器的所有目錄，請使用語法 *linked_server* (其中底線分隔符號是名稱規格的一部分)。 這個語法相當於針對目錄名稱限制指定 NULL，而且也會在連結的伺服器指出不支援目錄的資料來源時使用。  
 
 OLE DB Driver for SQL Server 會定義結構描述資料列集 LINKEDSERVERS，並傳回註冊成連結伺服器之 OLE DB 資料來源的清單。  
  
## <a name="see-also"></a>另請參閱  
 [結構描述資料列集支援 &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 資料列集 &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
