---
title: ISSAsynchStatus (OLE DB) |Microsoft 文件
description: ISSAsynchStatus (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 6c6ce6c399798206fc9f66af68bd1cf2ffea718a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSAsynchStatus**介面會公開支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]非同步作業。 它是選擇性的介面繼承自核心的 OLE DB 介面**IDBAsynchStatus**。 除了**中止**和**GetStatus**方法繼承自**IDBAsynchStatus**， **ISSAsynchStatus**提供一種新方法用來等候非同步作業已完成或發生逾時。  
  
|方法|Description|  
|------------|-----------------|  
|[Issasynchstatus:: Abort &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-abort-ole-db.md)|取消非同步執行的作業。|  
|[Issasynchstatus:: Getstatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|傳回以非同步方式執行作業的狀態。|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|等到非同步執行的作業完成或發生逾時為止。|  
  
## <a name="remarks"></a>備註  
 **ISSAsynchStatus**實作**issasynchstatus:: Getstatus**方法等同於**idbasynchstatus:: Getstatus**以外，如果方法資料來源物件的初始化已中止時，會傳回 E_UNEXPECTED 而不是 DB_E_CANCELED (雖然**issasynchstatus:: Waitforasynchcompletion**傳回 DB_E_CANCELED)。 這是因為資料來源物件未處於一般狀態之後中止作業，以便進行進一步的初始化作業。  
  
 下列方法支援在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中使用非同步執行：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>另請參閱  
 [介面 & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [執行非同步作業](../../oledb/features/performing-asynchronous-operations.md)  
  
  
