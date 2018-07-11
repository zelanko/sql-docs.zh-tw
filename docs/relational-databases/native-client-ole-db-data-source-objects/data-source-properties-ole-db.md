---
title: 資料來源屬性 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 6e14fefc-4e0b-4847-a833-4cf0abe65d50
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f108559bebad1ab98fc0c81ce0492293a9632e5b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419322"
---
# <a name="data-source-properties-ole-db"></a>資料來源屬性 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會實作資料來源屬性，如下所示。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|R/W：讀取/寫入 預設值：無<br /><br /> 描述： DBPROP_CURRENTCATALOG 的值會報告目前資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者工作階段。 設定屬性值已設定目前的資料庫使用相同的效果[!INCLUDE[tsql](../../includes/tsql-md.md)]使用*資料庫*陳述式。<br /><br /> 開頭[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，如果您呼叫[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)並指定資料庫名稱在較低的情況下，即使資料庫最初建立混合式案例的名稱，DBPROP_CURRENTCATALOG 會傳回小寫名稱。 使用舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，DBPROP_CURRENTCATALOG 會傳回預期的混合大小寫。|  
|DBPROP_MULTIPLECONNECTIONS|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：如果連接執行的命令不會產生資料列集，或者產生的資料列集不是伺服器資料指標，而且您執行其他命令，當 DBPROP_MULTIPLECONNECTIONS 為 VARIANT_TRUE 時，將會建立一個新的連接來執行新命令。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會建立另一個連接，如果 DBPROP_MULTIPLECONNECTION 為 VARIANT_FALSE，或如果交易在連接上作用。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回 db_e_objectopen，而如果 DBPROP_MULTIPLECONNECTIONS 為 VARIANT_FALSE，而且如果沒有使用中交易，傳回 E_FAIL。 交易與鎖定是以連接為基礎，由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理。 如果產生另一個連接，個別連接上的命令不會共用鎖定。 為確保命令之間不會互相封鎖，保留另一個命令要求之資料列上的鎖定。 建立多個工作階段時也是如此。<br /><br /> 每個工作階段都有一個個別的連接。|  
  
 在提供者專用的屬性集 DBPROPSET_SQLSERVERDATASOURCE 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會定義下列額外的資料來源屬性。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：若要從記憶體中啟用大量複製，SSPROP_ENABLEFASTLOAD 屬性應該設定為 VARIANT_TRUE。 資料來源上設定此屬性，新建立的工作階段可讓取用者存取權[IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)介面。<br /><br /> 如果屬性設定為 VARIANT_TRUE **IRowsetFastLoad**介面是可透過**iopenrowset:: Openrowset**藉由要求**ssprop_irowsetfastload**介面，或藉由設定**SSPROP_IRowsetFastLoad**為 VARIANT_TRUE。|  
|SSPROP_ENABLEBULKCOPY|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：若要從檔案中啟用大量複製，SSPROP_ENABLEBULKCOPY 屬性應該設定為 VARIANT_TRUE。 在資料來源上設定此屬性之後，取用者對於 IBCPSession 介面的存取會在與 Sessions 相同的層級下取得。<br /><br /> SSPROP_IRowsetFastLoad 也必須設定為 VARIANT_TRUE。|  
  
## <a name="see-also"></a>另請參閱  
 [資料來源物件&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
