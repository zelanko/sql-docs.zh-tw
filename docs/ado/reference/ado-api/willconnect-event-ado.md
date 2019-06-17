---
title: WillConnect 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 01b5c20668f97c80ae5abdcbb213914c012c7359
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710054"
---
# <a name="willconnect-event-ado"></a>WillConnect 事件 (ADO)
**WillConnect**連線開始前，會呼叫事件。  
  
 **適用於：** [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 A**字串**，其中包含暫止連接的連接資訊。  
  
 *UserID*  
 A**字串**，其中包含暫止連線的使用者名稱。  
  
 *密碼*  
 A**字串**，其中包含暫止連線的密碼。  
  
 *選項。*  
 A**長**值，指出提供者應該如何評估*ConnectionString*。 您只能選擇**adAsyncOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 呼叫此事件時，此參數設為**adStatusOK**預設。 它會設定為**adStatusCantDeny**如果事件無法要求取消暫止的作業。  
  
 這個事件會傳回之前，請將此參數設定為**adStatusUnwantedEvent**以避免後續的通知。 將此參數設定為**adStatusCancel**要求造成此通知的取消連接作業。  
  
 *pConnection*  
 [連線](../../../ado/reference/ado-api/connection-object-ado.md)物件套用此事件通知。 變更的參數**連接**依**WillConnect**事件處理常式不會影響**連接**。  
  
## <a name="remarks"></a>備註  
 當**WillConnect**呼叫時， *ConnectionString*， *UserID*，*密碼*，以及*選項*參數會設定為建立方法的作業，導致此事件 （暫止的連接），並可以在之前的事件會傳回變更的值。 **WillConnect**可能會傳回取消暫止連接要求。  
  
 當取消這個事件時， **ConnectComplete**用來呼叫其*adStatus*參數設定為**adStatusErrorsOccurred**。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
