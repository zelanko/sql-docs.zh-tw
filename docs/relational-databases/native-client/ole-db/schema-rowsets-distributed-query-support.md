---
title: 結構描述資料列集中的分散式查詢支援 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: daf4f4c0c7c6c1d53c2ab899dd150756399d53a3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296962"
---
# <a name="schema-rowsets---distributed-query-support"></a>結構描述資料列集 - 分散式查詢支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  為了支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]分散式查詢[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 本機用戶端 OLE 資料庫提供程式**IDBSchemaRowset**介面傳回連結伺服器上的中繼資料。  
  
 如果 DBPROPSET_SQLSERVERSESSION 屬性 SSPROP_QUOTEDCATALOGNAMES 是 VARIANT_TRUE，您就可以針對目錄名稱指定引號識別碼 (例如 "my.catalog")。 依目錄限制架構列集輸出時,[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式會識別包含連結伺服器和目錄名稱的兩部分名稱。 對下表中的架構列集,將兩部份目錄名稱指定為_linked_server_**。**_目錄_將輸出限制為命名連結伺服器的適用目錄。  
  
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
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式定義架構列集連結伺服器,返回註冊為連結伺服器的 OLE DB 資料來源的清單。  
  
## <a name="see-also"></a>另請參閱  
 [架構排集支援&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 資料列集 &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
