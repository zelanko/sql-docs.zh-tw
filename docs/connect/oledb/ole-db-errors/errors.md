---
title: 錯誤 |Microsoft Docs
description: 錯誤
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: cbc69702105ece1e2406ebda9be4f906cc27585a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643086"
---
# <a name="errors"></a>錯誤
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE/COM 物件會透過物件成員函數的 HRESULT 傳回碼報告錯誤。 OLE/COM HRESULT 是一個位元封裝的結構。 OLE 會提供為結構成員取值 (Dereference) 的巨集。  
  
 OLE/COM 會指定 **IErrorInfo** 介面。 介面會公開方法，例如 **GetDescription**。 這可讓用戶端從 OLE/COM 伺服器擷取錯誤詳細資料。 OLE DB 會擴充 **IErrorInfo**，在執行單一成員函數時，支援傳回多個錯誤資訊封包。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以傳回多個錯誤。 應用程式可以呼叫與 ISQLErrorInfo 和 IErrorRecords 結合的 [IMultipleResults::GetResult](http://go.microsoft.com/fwlink/?LinkId=129630)，一次擷取一個伺服器錯誤。  
  
 OLE DB Driver for SQL Server 會公開 OLE DB 記錄加強的 **IErrorInfo**、自訂 **ISQLErrorInfo**，以及提供者特定的 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 錯誤物件介面。  
  
 如需追蹤錯誤的資訊，請參閱 [Data Access Tracing](http://go.microsoft.com/fwlink/?LinkId=125805) (資料存取追蹤)。 如需在中新增的錯誤追蹤增強功能[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，請參閱 <<c2> [ 存取擴充事件記錄檔中的診斷資訊](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [傳回碼](../../oledb/ole-db-errors/return-codes.md)  
  
-   [錯誤介面中的資訊](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server 錯誤詳細資料](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [擷取錯誤資訊](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server 訊息結果](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 程式設計](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
