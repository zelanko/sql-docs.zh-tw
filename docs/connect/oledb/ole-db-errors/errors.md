---
title: 錯誤 |Microsoft 文件
description: 錯誤
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ea14d636771de6edb42d41876c5d94489ce6199
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2018
---
# <a name="errors"></a>錯誤
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE/COM 物件會透過物件成員函數的 HRESULT 傳回碼報告錯誤。 OLE/COM HRESULT 是一個位元封裝的結構。 OLE 會提供為結構成員取值 (Dereference) 的巨集。  
  
 OLE/COM 會指定**IErrorInfo**介面。 介面會公開方法例如**GetDescription**。 這可讓用戶端從 OLE/COM 伺服器擷取錯誤詳細資料。 OLE DB 會擴充**IErrorInfo**支援傳回多個錯誤資訊封包的單一成員函式執行。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以傳回多個錯誤。 應用程式可以擷取一個伺服器錯誤一次呼叫[imultipleresults:: Getresult](http://go.microsoft.com/fwlink/?LinkId=129630) ISQLErrorInfo 與 IErrorRecords 結合。  
  
 SQL Server OLE DB 驅動程式會公開 OLE DB 記錄加強**IErrorInfo**，自訂**ISQLErrorInfo**，和提供者特定[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)錯誤物件介面。  
  
 追蹤錯誤的相關資訊，請參閱[資料存取追蹤](http://go.microsoft.com/fwlink/?LinkId=125805)。 錯誤追蹤中新增的增強功能相關資訊的[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，請參閱[存取擴充事件記錄檔中的診斷資訊](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [傳回碼](../../oledb/ole-db-errors/return-codes.md)  
  
-   [錯誤介面中的資訊](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server 錯誤詳細資料](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [擷取錯誤資訊](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server 訊息結果](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 的 OLE DB 驅動程式&#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
  
  
