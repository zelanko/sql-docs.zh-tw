---
title: 工作階段屬性 - OLE DB Driver for SQL Server | Microsoft Docs
description: 工作階段屬性 - OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- OLE DB Driver for SQL Server, sessions
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 9cefecde35d33b9bf400b5af014756f2ddd09a58
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47660426"
---
# <a name="session-properties---ole-db-driver-for-sql-server"></a>工作階段屬性 - OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server OLE DB 工作階段會將屬性解譯如下。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|OLE DB Driver for SQL Server 支援所有自動認可交易隔離等級，但是混亂等級 DBPROPVAL_TI_CHAOS 除外。|  
  
 在提供者特定的屬性集 DBPROPSET_SQLSERVERSESSION 中，OLE DB Driver for SQL Server 會定義下列其他工作階段屬性。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|類型：VT_BOOL<br /><br /> R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：CATALOG 限制中允許引號識別碼。<br /><br /> VARIANT_TRUE：辨識出引號識別碼有提供分散式查詢支援之結構描述資料列集的目錄限制。<br /><br /> VARIANT_FALSE：未辨識出引號識別碼有提供分散式查詢支援之結構描述資料列集的目錄限制。<br /><br /> 如需提供分散式查詢支援之結構描述資料列集的詳細資訊，請參閱[結構描述資料列集中的分散式查詢支援](../../oledb/ole-db/schema-rowsets-distributed-query-support.md)。|  
|SSPROP_ALLOWNATIVEVARIANT|類型：VT_BOOL<br /><br /> R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：決定所提取的資料是否為 DBTYPE_VARIANT 或 DBTYPE_SQLVARIANT。<br /><br /> VARIANT_TRUE：資料行類型是以 DBTYPE_SQLVARIANT 傳回，在此種情況下，緩衝區會保存 SSVARIANT 結構。<br /><br /> VARIANT_FALSE：資料行類型是以 DBTYPE_VARIANT 傳回，而且緩衝區將具有 VARIANT 結構。|  
|SSPROP_ASYNCH_BULKCOPY|若要使用非同步模式，請在呼叫 BCPExec 方法之前將提供者特有的工作階段屬性 SSPROP_ASYNCH_BULKCOPY 設定為 VARIANT_TRUE。 DBPROPSET_SQLSERVERSESSION 屬性集中有提供這個屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料來源物件&#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
