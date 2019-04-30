---
title: 錯誤 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
ms.assetid: bd0612f4-96ef-4919-b0f9-b5447210fe93
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 434b4251c51809c97744e7aaf954ac1f11c06cfa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63050670"
---
# <a name="errors"></a>錯誤
  OLE/COM 物件會透過物件成員函數的 HRESULT 傳回碼報告錯誤。 OLE/COM HRESULT 是一個位元封裝的結構。 OLE 會提供為結構成員取值 (Dereference) 的巨集。  
  
 OLE/COM 會指定 **IErrorInfo** 介面。 介面會公開方法，例如 **GetDescription**。 這可讓用戶端從 OLE/COM 伺服器擷取錯誤詳細資料。 OLE DB 會擴充 **IErrorInfo**，在執行單一成員函數時，支援傳回多個錯誤資訊封包。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以傳回多個錯誤。 應用程式可以呼叫與 ISQLErrorInfo 和 IErrorRecords 結合的 [IMultipleResults::GetResult](https://go.microsoft.com/fwlink/?LinkId=129630)，一次擷取一個伺服器錯誤。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開 OLE DB 記錄加強**IErrorInfo**，自訂`ISQLErrorInfo`，和提供者特定[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)物件時發生錯誤介面。  
  
 如需追蹤錯誤的資訊，請參閱 [Data Access Tracing](https://go.microsoft.com/fwlink/?LinkId=125805) (資料存取追蹤)。 如需在中新增的錯誤追蹤增強功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，請參閱 <<c2> [ 存取擴充事件記錄檔中的診斷資訊](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [傳回碼](return-codes.md)  
  
-   [錯誤介面中的資訊](information-in-error-interfaces.md)  
  
-   [SQL Server 錯誤詳細資料](sql-server-error-detail.md)  
  
-   [擷取錯誤資訊](retrieving-error-information.md)  
  
-   [SQL Server 訊息結果](sql-server-message-results.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
