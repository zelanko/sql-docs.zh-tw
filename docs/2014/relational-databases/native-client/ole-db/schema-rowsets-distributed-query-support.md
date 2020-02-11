---
title: 架構資料列集中的分散式查詢支援 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 24411ceb757414f1a70f0f10bdf5b2c7660e2cd8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62667594"
---
# <a name="distributed-query-support-in-schema-rowsets"></a>結構描述資料列集中的分散式查詢支援
  為了支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]分散式查詢， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者**IDBSchemaRowset**介面會傳回連結伺服器上的中繼資料。  
  
 如果 DBPROPSET_SQLSERVERSESSION 屬性 SSPROP_QUOTEDCATALOGNAMES 是 VARIANT_TRUE，您就可以針對目錄名稱指定引號識別碼 (例如 "my.catalog")。 當根據目錄來限制架構資料列集[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]輸出時，Native Client OLE DB 提供者會辨識包含連結伺服器和目錄名稱的兩部分名稱。 針對下表中的架構資料列集，將兩部分的目錄名稱指定為_linked_server_**。**_目錄_會將輸出限制為所指定連結伺服器的適用類別目錄。  
  
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
>  若要將結構描述資料列集限制為連結伺服器的所有目錄，請使用語法 *linked_server* (其中句號分隔符號是名稱規格的一部分)。 這個語法相當於針對目錄名稱限制指定 NULL，而且也會在連結的伺服器指出不支援目錄的資料來源時使用。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會定義架構資料列集 LINKEDSERVERS，並傳回註冊為連結伺服器之 OLE DB 資料來源的清單。  
  
## <a name="see-also"></a>另請參閱  
 [架構資料列集支援 &#40;OLE DB&#41;](schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 資料列集 &#40;OLE DB&#41;](schema-rowsets-linkedservers-rowset.md)  
  
  
