---
title: 錯誤 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d86f421600c392f1ccc43d35ae293725c9d82bcf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47775966"
---
# <a name="errors"></a>錯誤
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  OLE/COM 物件會透過物件成員函數的 HRESULT 傳回碼報告錯誤。 OLE/COM HRESULT 是一個位元封裝的結構。 OLE 會提供為結構成員取值 (Dereference) 的巨集。  
  
 OLE/COM 會指定 **IErrorInfo** 介面。 介面會公開方法，例如 **GetDescription**。 這可讓用戶端從 OLE/COM 伺服器擷取錯誤詳細資料。 OLE DB 會擴充 **IErrorInfo**，在執行單一成員函數時，支援傳回多個錯誤資訊封包。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以傳回多個錯誤。 應用程式可以呼叫與 ISQLErrorInfo 和 IErrorRecords 結合的 [IMultipleResults::GetResult](http://go.microsoft.com/fwlink/?LinkId=129630)，一次擷取一個伺服器錯誤。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開 OLE DB 記錄加強**IErrorInfo**，自訂**ISQLErrorInfo**，和提供者特定[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)錯誤物件介面。  
  
 如需追蹤錯誤的資訊，請參閱 [Data Access Tracing](http://go.microsoft.com/fwlink/?LinkId=125805) (資料存取追蹤)。 如需在中新增的錯誤追蹤增強功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，請參閱 <<c2> [ 存取擴充事件記錄檔中的診斷資訊](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [傳回碼](../../relational-databases/native-client-ole-db-errors/return-codes.md)  
  
-   [錯誤介面中的資訊](../../relational-databases/native-client-ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server 錯誤詳細資料](../../relational-databases/native-client-ole-db-errors/sql-server-error-detail.md)  
  
-   [擷取錯誤資訊](../../relational-databases/native-client-ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server 訊息結果](../../relational-databases/native-client-ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
