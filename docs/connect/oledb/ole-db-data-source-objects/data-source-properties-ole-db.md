---
title: 資料來源屬性 (OLE DB) |Microsoft 文件
description: 資料來源屬性 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ef755447b9bb515fa6d05e1628ce7504e79f804a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-properties-ole-db"></a>資料來源屬性 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server OLE DB 驅動程式會實作資料來源屬性，如下所示。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|R/W：讀取/寫入 預設值：無<br /><br /> 描述： DBPROP_CURRENTCATALOG 的值會報告目前資料庫的 OLE DB 驅動程式 SQL Server 工作階段。 設定屬性值已設定目前的資料庫使用相同的效果[!INCLUDE[tsql](../../../includes/tsql-md.md)]使用*資料庫*陳述式。<br /><br /> 開頭為[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，如果您呼叫[sp_defaultdb](../../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) ，並指定資料庫名稱在較低的情況下，即使資料庫最初建立混合式案例的名稱，DBPROP_CURRENTCATALOG 會傳回以小寫的名稱。 使用舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，DBPROP_CURRENTCATALOG 會傳回預期的混合大小寫。|  
|DBPROP_MULTIPLECONNECTIONS|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：如果連接執行的命令不會產生資料列集，或者產生的資料列集不是伺服器資料指標，而且您執行其他命令，當 DBPROP_MULTIPLECONNECTIONS 為 VARIANT_TRUE 時，將會建立一個新的連接來執行新命令。<br /><br /> 如果 DBPROP_MULTIPLECONNECTION 為 VARIANT_FALSE，或者如果交易在連接上作用中，SQL Server OLE DB 驅動程式將不會建立其他連接。 SQL Server OLE DB 驅動程式會傳回 db_e_objectopen，而如果 DBPROP_MULTIPLECONNECTIONS 為 VARIANT_FALSE，而且如果沒有使用中交易時，傳回 E_FAIL。 交易與鎖定是以連接為基礎，由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理。 如果產生另一個連接，個別連接上的命令不會共用鎖定。 為確保命令之間不會互相封鎖，保留另一個命令要求之資料列上的鎖定。 建立多個工作階段時也是如此。<br /><br /> 每個工作階段都有一個個別的連接。|  
  
 在提供者特有的屬性集 DBPROPSET_SQLSERVERDATASOURCE 中，SQL Server OLE DB 驅動程式會定義下列額外的資料來源屬性。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：若要從記憶體中啟用大量複製，SSPROP_ENABLEFASTLOAD 屬性應該設定為 VARIANT_TRUE。 資料來源上設定此屬性，新建立的工作階段可讓取用者存取[IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)介面。<br /><br /> 如果屬性設定為 VARIANT_TRUE， **IRowsetFastLoad**介面是可透過**iopenrowset:: Openrowset**要求**ssprop_irowsetfastload**介面，或是藉由設定**SSPROP_IRowsetFastLoad**為 VARIANT_TRUE。|  
|SSPROP_ENABLEBULKCOPY|R/W：讀取/寫入 預設值：VARIANT_FALSE<br /><br /> 描述：若要從檔案中啟用大量複製，SSPROP_ENABLEBULKCOPY 屬性應該設定為 VARIANT_TRUE。 在資料來源上設定此屬性之後，取用者對於 IBCPSession 介面的存取會在與 Sessions 相同的層級下取得。<br /><br /> SSPROP_IRowsetFastLoad 也必須設定為 VARIANT_TRUE。|  
  
## <a name="see-also"></a>另請參閱  
 [資料來源物件 & #40; OLE DB & #41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
