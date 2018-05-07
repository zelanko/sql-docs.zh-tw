---
title: 使用快照隔離 |Microsoft 文件
description: 使用 SQL Server 的 OLE DB 驅動程式中的快照集隔離
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 7c70ad99b77f4dc70329d86adc936f18faced890
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-snapshot-isolation"></a>使用快照隔離
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引進了新的「快照」隔離等級，目的是增強線上交易處理 (OLTP) 應用程式的並行存取。 在舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，並行存取完全以鎖定為基礎，因此導致某些應用程式發生封鎖及死結問題。 快照集隔離相依於對資料列版本設定的增強功能，目的是藉由避免發生讀取器-寫入器封鎖的案例來改善效能。  
  
 在快照隔離下啟動的交易會根據交易啟動的時間而讀取資料庫快照。 索引鍵集、 動態和靜態伺服器資料指標中，開啟快照集交易內容的行為與可序列化交易內所開啟的靜態資料指標類似。 不過，當資料指標開啟時不會採用快照集隔離層級鎖定。 這項事實可以降低在伺服器上進行封鎖。  
  
## <a name="ole-db-driver-for-sql-server"></a>SQL Server 的 OLE DB 驅動程式  
 SQL Server OLE DB 驅動程式的增強功能可利用中所引進的快照集隔離[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 這些增強功能包括對 DBPROPSET_DATASOURCEINFO 和 DBPROPSET_SESSION 屬性集所做的變更。  
  
### <a name="dbpropsetdatasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 DBPROPSET_DATASOURCEINFO 屬性集已變更，現藉由加入用於 DBPROP_SUPPORTEDTXNISOLEVELS 屬性中的 DBPROPVAL_TI_SNAPSHOT 值來支援快照隔離等級。 這個新值代表不論資料庫上是否啟用版本控制，快照隔離等級都受到支援。 下表列出 DBPROP_SUPPORTEDTXNISOLEVELS 值：  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|類型：VT_I4<br /><br /> R/W：唯讀<br /><br /> 說明：指定受支援之交易隔離等級的位元遮罩。 下列零或多個項目的組合：<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropsetsession"></a>DBPROPSET_SESSION  
 DBPROPSET_SESSION 屬性集已變更，現藉由加入用於 DBPROP_SESS_AUTOCOMMITISOLEVELS 屬性中的 DBPROPVAL_TI_SNAPSHOT 值來支援快照隔離等級。 這個新值代表不論資料庫上是否啟用版本控制，快照隔離等級都受到支援。 下表列出 DBPROP_SESS_AUTOCOMMITISOLEVELS 值：
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|類型：VT_I4<br /><br /> R/W：唯讀<br /><br /> 說明：指定自動認可模式時之交易隔離等級的位元遮罩。 您可以將這個位元遮罩的值都可以針對 dbprop_supportedtxnisolevels 而設定的值相同。|  
  
> [!NOTE]  
>  如果使用早於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 版本時設定 DBPROPVAL_TI_SNAPSHOT，就會發生 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED 錯誤。  
  
 如需如何在交易中支援快照隔離的資訊，請參閱[支援本機交易](../../oledb/ole-db-transactions/supporting-local-transactions.md)。  

  
## <a name="see-also"></a>另請參閱  
 [SQL Server 功能的 OLE DB 驅動程式](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [資料列集屬性和行為](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
