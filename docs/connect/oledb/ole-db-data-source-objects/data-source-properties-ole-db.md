---
title: 資料來源屬性 (OLE DB) |Microsoft Docs
description: 資料來源屬性 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 13dd6afde96d42ac1fcc82b6fb24c721997b951d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015928"
---
# <a name="data-source-properties-ole-db"></a>資料來源屬性 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 的 OLE DB 驅動程式會執行資料來源屬性, 如下所示。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|R/W：讀取/寫入 預設值：無<br /><br /> 描述：DBPROP_CURRENTCATALOG 的值會針對 OLE DB Driver for SQL Server 工作階段報告目前的資料庫。 設定屬性值的效果與使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] USE *database* 陳述式設定目前資料庫的效果相同。<br /><br /> 從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 開始，如果您呼叫 [sp_defaultdb](../../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) 並以小寫指定資料庫名稱，即使資料庫原始是以混合大小寫的名稱建立，DBPROP_CURRENTCATALOG 也會以小寫傳回名稱。 使用舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，DBPROP_CURRENTCATALOG 會傳回預期的混合大小寫。|  
|DBPROP_MULTIPLECONNECTIONS|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：如果連接執行的命令不會產生資料列集，或者產生的資料列集不是伺服器資料指標，而且您執行其他命令，當 DBPROP_MULTIPLECONNECTIONS 為 VARIANT_TRUE 時，將會建立一個新的連接來執行新命令。<br /><br /> 如果 DBPROP_MULTIPLECONNECTION 為 VARIANT_FALSE，或者如果交易在連接上作用中，OLE DB Driver for SQL Server 將不會建立其他連接。 如果 DBPROP_MULTIPLECONNECTIONS 為 VARIANT_FALSE，OLE DB Driver for SQL Server 會傳回 DB_E_OBJECTOPEN，而如果有作用中的交易，則傳回 E_FAIL。 交易與鎖定是以連接為基礎，由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理。 如果產生另一個連接，個別連接上的命令不會共用鎖定。 為確保命令之間不會互相封鎖，保留另一個命令要求之資料列上的鎖定。 建立多個工作階段時也是如此。<br /><br /> 每個工作階段都有一個個別的連接。|  
  
 在提供者特定的屬性集 DBPROPSET_SQLSERVERDATASOURCE 中，OLE DB Driver for SQL Server 會定義下列其他資料來源屬性。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：若要從記憶體中啟用大量複製，SSPROP_ENABLEFASTLOAD 屬性應該設定為 VARIANT_TRUE。 在資料來源上設定此屬性之後，新建立的工作階段就會允許取用者存取 [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) 介面。<br /><br /> 如果屬性設定為 VARIANT_TRUE，**IRowsetFastLoad** 介面會要求 **IID_IRowsetFastLoad** 介面，或將 **SSPROP_IRowsetFastLoad** 設定為 VARIANT_TRUE，以便透過 **IOpenRowset::OpenRowset** 取得。|  
|SSPROP_ENABLEBULKCOPY|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：若要從檔案中啟用大量複製，SSPROP_ENABLEBULKCOPY 屬性應該設定為 VARIANT_TRUE。 在資料來源上設定此屬性之後，取用者對於 IBCPSession 介面的存取會在與 Sessions 相同的層級下取得。<br /><br /> SSPROP_IRowsetFastLoad 也必須設定為 VARIANT_TRUE。|  
  
## <a name="see-also"></a>另請參閱  
 [資料來源物件&#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
