---
title: 資料來源屬性 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 6e14fefc-4e0b-4847-a833-4cf0abe65d50
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 58df10e434bff0213ca9961c91e51e38aadd03bf
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002749"
---
# <a name="data-source-properties-ole-db"></a>資料來源屬性 (OLE DB)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會依照下列方式實作為資料來源屬性。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|R/W：讀取/寫入 預設值：無<br /><br /> 描述： DBPROP_CURRENTCATALOG 的值會報告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會話的目前資料庫。 設定屬性值的效果與使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] USE *database* 陳述式設定目前資料庫的效果相同。<br /><br /> 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，如果您呼叫 [sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) 並以小寫指定資料庫名稱，即使資料庫原始是以混合大小寫的名稱建立，DBPROP_CURRENTCATALOG 也會以小寫傳回名稱。 使用舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，DBPROP_CURRENTCATALOG 會傳回預期的混合大小寫。|  
|DBPROP_MULTIPLECONNECTIONS|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：如果連接執行的命令不會產生資料列集，或者產生的資料列集不是伺服器資料指標，而且您執行其他命令，當 DBPROP_MULTIPLECONNECTIONS 為 VARIANT_TRUE 時，將會建立一個新的連接來執行新命令。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果 DBPROP_MULTIPLECONNECTION VARIANT_FALSE，或者如果交易在連接上作用中，Native Client OLE DB 提供者就不會建立另一個連接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果 VARIANT_FALSE DBPROP_MULTIPLECONNECTIONS，Native Client OLE DB 提供者會傳回 DB_E_OBJECTOPEN，如果有使用中的交易，則會傳回 E_FAIL。 交易與鎖定是以連接為基礎，由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理。 如果產生另一個連接，個別連接上的命令不會共用鎖定。 為確保命令之間不會互相封鎖，保留另一個命令要求之資料列上的鎖定。 建立多個工作階段時也是如此。<br /><br /> 每個工作階段都有一個個別的連接。|  
  
 在提供者特定的屬性集 DBPROPSET_SQLSERVERDATASOURCE 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會定義下列額外的資料來源屬性。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：若要從記憶體中啟用大量複製，SSPROP_ENABLEFASTLOAD 屬性應該設定為 VARIANT_TRUE。 在資料來源上設定此屬性之後，新建立的工作階段就會允許取用者存取 [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) 介面。<br /><br /> 如果屬性設定為 VARIANT_TRUE，**IRowsetFastLoad** 介面會要求 **IID_IRowsetFastLoad** 介面，或將 **SSPROP_IRowsetFastLoad** 設定為 VARIANT_TRUE，以便透過 **IOpenRowset::OpenRowset** 取得。|  
|SSPROP_ENABLEBULKCOPY|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：若要從檔案中啟用大量複製，SSPROP_ENABLEBULKCOPY 屬性應該設定為 VARIANT_TRUE。 在資料來源上設定此屬性之後，取用者對於 IBCPSession 介面的存取會在與 Sessions 相同的層級下取得。<br /><br /> SSPROP_IRowsetFastLoad 也必須設定為 VARIANT_TRUE。|  
  
## <a name="see-also"></a>另請參閱  
 [資料來源物件 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
