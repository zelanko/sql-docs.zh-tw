---
title: "ISSAsynchStatus (OLE DB) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords: ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f97d1ca363452b6f8b91cc1d70794df200539e7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **ISSAsynchStatus**公開支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]非同步作業。 這是選擇性的介面，繼承自核心的 OLE DB 介面**IDBAsynchStatus**。 除了**中止**和**GetStatus**方法繼承自**IDBAsynchStatus**， **ISSAsynchStatus**提供一種新方法用來等候非同步作業已完成或發生逾時。  
  
|方法|Description|  
|------------|-----------------|  
|[Issasynchstatus:: Abort &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md)|取消非同步執行的作業。|  
|[Issasynchstatus:: Getstatus &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|傳回以非同步方式執行作業的狀態。|  
|[Issasynchstatus:: Waitforasynchcompletion &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|等到非同步執行的作業完成或發生逾時為止。|  
  
## <a name="remarks"></a>備註  
 **ISSAsynchStatus**實作**issasynchstatus:: Getstatus**方法等同於**idbasynchstatus:: Getstatus**以外，如果方法資料來源物件的初始化已中止時，會傳回 E_UNEXPECTED 而不是 DB_E_CANCELED (雖然**issasynchstatus:: Waitforasynchcompletion**傳回 DB_E_CANCELED)。 這是因為資料來源物件在中止作業後不會保留在一般的狀態，如此可以讓系統嘗試進一步的初始化作業。  
  
 下列方法支援在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用非同步執行：  
  
-   **Icommand:: Execute**  
  
-   **Iopenrowset:: Openrowset**  
  
-   **Imultipleresults:: Getresult**  
  
## <a name="see-also"></a>請參閱＜  
 [介面 &#40; OLE DB &#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [執行非同步作業](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
