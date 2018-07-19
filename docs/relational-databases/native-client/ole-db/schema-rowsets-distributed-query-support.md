---
title: 分散式查詢支援，在結構描述資料列 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4787efa0905f0a54d70cf02af19328af13f70e6c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420987"
---
# <a name="schema-rowsets---distributed-query-support"></a>結構描述資料列集-分散式的查詢支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  若要支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]分散式查詢中， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者**IDBSchemaRowset**介面會傳回連結伺服器上的中繼資料。  
  
 如果 DBPROPSET_SQLSERVERSESSION 屬性 SSPROP_QUOTEDCATALOGNAMES 是 VARIANT_TRUE，您就可以針對目錄名稱指定引號識別碼 (例如 "my.catalog")。 依照目錄來限制結構描述資料列集輸出時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會辨識包含連結的伺服器和目錄名稱的兩部分名稱。 下表中的結構描述資料列集，指定兩部分目錄名稱，作為*linked_server ***。*** 目錄*將輸出限制為具名連結伺服器的適用目錄。  
  
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
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會定義結構描述資料列集 LINKEDSERVERS，並傳回註冊成連結伺服器的 OLE DB 資料來源的清單。  
  
## <a name="see-also"></a>另請參閱  
 [結構描述資料列集支援&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 資料列集&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
