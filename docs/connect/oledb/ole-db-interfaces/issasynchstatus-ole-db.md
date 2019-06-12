---
title: ISSAsynchStatus (OLE DB) |Microsoft Docs
description: ISSAsynchStatus (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 2ad9f5ad8912d6e820c237d51c02ff10066a302a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66784013"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **ISSAsynchStatus** 介面會公開對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 非同步作業的支援。 這是選擇性的介面，繼承自核心的 OLE DB 介面 **IDBAsynchStatus**。 除了繼承自 **IDBAsynchStatus** 的 **Abort** 和 **GetStatus** 方法之外，**ISSAsynchStatus** 還提供一個新方法，用來等到非同步作業完成或發生逾時。  
  
|方法|Description|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-abort-ole-db.md)|取消非同步執行的作業。|  
|[ISSAsynchStatus::GetStatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|傳回以非同步方式執行作業的狀態。|  
|[ISSAsynchStatus::WaitForAsynchCompletion &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|等到非同步執行的作業完成或發生逾時為止。|  
  
## <a name="remarks"></a>Remarks  
 **ISSAsynchStatus::GetStatus** 方法的 **ISSAsynchStatus** 實作與 **IDBAsynchStatus::GetStatus** 方法相同，不同的是如果中止資料來源物件的初始化，便會傳回 E_UNEXPECTED，而不是 DB_E_CANCELED (雖然 **ISSAsynchStatus::WaitForAsynchCompletion** 會傳回 DB_E_CANCELED)。 這是因為資料來源物件在中止作業後不會保留在一般的狀態，如此可以讓系統嘗試進一步的初始化作業。  
  
 下列方法支援在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中使用非同步執行：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [執行非同步作業](../../oledb/features/performing-asynchronous-operations.md)  
  
  
