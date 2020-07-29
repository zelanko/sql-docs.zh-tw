---
title: 使用快照集隔離 | Microsoft Docs
description: 在 OLE DB Driver for SQL Server 中使用快照集隔離
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], snapshot isolation
- MSOLEDBSQL, snapshot isolation
- isolation levels [SQL Server], snapshot
- DBPROPSET_SESSION property set
- DBDROPSET_DATASOURCEINFO property set
- snapshot isolation [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, snapshot isolation
- SQLGetInfo function
- concurrency [OLE DB Driver for SQL Server]
- SQLSetConnectAttr function
author: pmasl
ms.author: pelopes
ms.openlocfilehash: acbb39726ede983d3c0909235d1fb2ddb588d65b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "85986514"
---
# <a name="working-with-snapshot-isolation"></a>使用快照隔離
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引進了新的「快照」隔離等級，目的是增強線上交易處理 (OLTP) 應用程式的並行存取。 在舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，並行存取完全以鎖定為基礎，因此導致某些應用程式發生封鎖及死結問題。 快照集隔離相依於對資料列版本設定的增強功能，目的是藉由避免發生讀取器-寫入器封鎖的案例來改善效能。  
  
 在快照隔離下啟動的交易會根據交易啟動的時間而讀取資料庫快照。 在快照交易內容中開啟的索引鍵集、動態和靜態伺服器資料指標的行為，與在可序列化交易中開啟的靜態資料指標非常類似。 不過，在快照隔離等級下開啟資料指標時，不會發生鎖定。 這項事實可以減少伺服器上的封鎖。  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server  
 OLE DB Driver for SQL Server 具備增強功能，可利用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中所引進的快照集隔離。 這些增強功能包括對 DBPROPSET_DATASOURCEINFO 和 DBPROPSET_SESSION 屬性集所做的變更。  
  
### <a name="dbpropset_datasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 DBPROPSET_DATASOURCEINFO 屬性集已變更，現藉由加入用於 DBPROP_SUPPORTEDTXNISOLEVELS 屬性中的 DBPROPVAL_TI_SNAPSHOT 值來支援快照隔離等級。 這個新值代表不論資料庫上是否啟用版本控制，快照隔離等級都受到支援。 下表列出 DBPROP_SUPPORTEDTXNISOLEVELS 值：  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|類型：VT_I4<br /><br /> R/W：唯讀<br /><br /> 說明：指定受支援之交易隔離等級的位元遮罩。 下列零或多個項目的組合：<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropset_session"></a>DBPROPSET_SESSION  
 DBPROPSET_SESSION 屬性集已變更，現藉由加入用於 DBPROP_SESS_AUTOCOMMITISOLEVELS 屬性中的 DBPROPVAL_TI_SNAPSHOT 值來支援快照隔離等級。 這個新值代表不論資料庫上是否啟用版本控制，快照隔離等級都受到支援。 下表列出 DBPROP_SESS_AUTOCOMMITISOLEVELS 值：
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|類型：VT_I4<br /><br /> R/W：唯讀<br /><br /> 說明：指定自動認可模式時之交易隔離等級的位元遮罩。 在此位元遮罩中設定的值，與針對 DBPROP_SUPPORTEDTXNISOLEVELS 而設定的值相同。|  
  
> [!NOTE]  
>  如果使用早於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 版本時設定 DBPROPVAL_TI_SNAPSHOT，就會發生 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED 錯誤。  
  
 如需如何在交易中支援快照集隔離的詳細資訊，請參閱[支援本機交易](../../oledb/ole-db-transactions/supporting-local-transactions.md)。  

  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [資料列集屬性和行為](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
