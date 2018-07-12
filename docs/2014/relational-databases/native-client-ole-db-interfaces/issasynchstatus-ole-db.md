---
title: ISSAsynchStatus (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSAsynchStatus (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a112c19d78c4d59b68ea5896109f88a101aaad13
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413403"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
  **ISSAsynchStatus**公開支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]非同步作業。 這是選擇性的介面，繼承自核心的 OLE DB 介面**IDBAsynchStatus**。 除了**中止**並**GetStatus**方法繼承自**IDBAsynchStatus**， **ISSAsynchStatus**提供一種新方法用來等到非同步作業已完成或發生逾時。  
  
|方法|描述|  
|------------|-----------------|  
|[Issasynchstatus:: Abort &#40;OLE DB&#41;](issasynchstatus-abort-ole-db.md)|取消非同步執行的作業。|  
|[Issasynchstatus:: Getstatus &#40;OLE DB&#41;](issasynchstatus-getstatus-ole-db.md)|傳回以非同步方式執行作業的狀態。|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](issasynchstatus-waitforasynchcompletion-ole-db.md)|等到非同步執行的作業完成或發生逾時為止。|  
  
## <a name="remarks"></a>備註  
 **ISSAsynchStatus**實作**issasynchstatus:: Getstatus**方法相當於**idbasynchstatus:: Getstatus**以外，如果方法資料來源物件的初始化已中止，會傳回 E_UNEXPECTED，而不是 DB_E_CANCELED (雖然**issasynchstatus:: Waitforasynchcompletion**會傳回 DB_E_CANCELED)。 這是因為資料來源物件在中止作業後不會保留在一般的狀態，如此可以讓系統嘗試進一步的初始化作業。  
  
 下列方法支援在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用非同步執行：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [執行非同步作業](../native-client/features/performing-asynchronous-operations.md)  
  
  
