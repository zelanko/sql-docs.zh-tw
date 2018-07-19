---
title: WillConnect 事件 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a2ddca516e9c5141e0e874074660579e8144ba7
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282867"
---
# <a name="willconnect-event-ado"></a>WillConnect 事件 (ADO)
**WillConnect**連線開始前，呼叫事件。  
  
 **適用於：** [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 A**字串**，其中包含暫止連線的連接資訊。  
  
 *使用者識別碼*  
 A**字串**，其中包含暫止連線的使用者名稱。  
  
 *密碼*  
 A**字串**，其中包含暫止連線的密碼。  
  
 *選項*  
 A**長**值，指出提供者應該如何評估*ConnectionString*。 唯一的選擇是**adAsyncOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當呼叫這個事件時，這個參數會設定為**adStatusOK**預設。 設定為**adStatusCantDeny**如果事件無法要求取消的暫止的作業。  
  
 這個事件會傳回之前，請將此參數設定為**adStatusUnwantedEvent**以避免後續的通知。 這個參數設定為**adStatusCancel**要求造成這項通知的取消的連接作業。  
  
 *pConnection*  
 [連接](../../../ado/reference/ado-api/connection-object-ado.md)套用此事件通知的物件。 變更的參數為**連接**由**WillConnect**事件處理常式不會影響**連接**。  
  
## <a name="remarks"></a>備註  
 當**WillConnect**呼叫時， *ConnectionString*， *UserID*，*密碼*，和*選項*參數是設定為造成此事件 （暫止的連接），可在之前的事件會傳回變更的作業所建立的值。 **WillConnect**取消暫止的連接要求可能會傳回。  
  
 當取消這個事件時， **ConnectComplete**用來呼叫其*adStatus*參數設定為**adStatusErrorsOccurred**。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
