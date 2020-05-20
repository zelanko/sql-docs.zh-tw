---
title: WillConnect 事件（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 73798796af7629e70dda86bd0e264ec325be8a0e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764459"
---
# <a name="willconnect-event-ado"></a>WillConnect 事件 (ADO)
**WillConnect**事件會在連接開始之前呼叫。  
  
 **適用于：** [CONNECTION 物件（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 包含暫止連接之連接資訊的**字串**。  
  
 *UserID*  
 包含暫止連接之使用者名稱的**字串**。  
  
 *密碼*  
 包含暫止連接之密碼的**字串**。  
  
 *選項*  
 指出提供者應該如何評估*ConnectionString*的**Long**值。 您的唯一選項是**adAsyncOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 呼叫這個事件時，預設會將此參數設定為**adStatusOK** 。 如果事件無法要求取消暫止的作業，則會設定為**adStatusCantDeny** 。  
  
 在此事件傳回之前，請將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。 將此參數設定為**adStatusCancel** ，以要求導致取消此通知的連接作業。  
  
 *pConnection*  
 套用此事件通知的[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。 **WillConnect**事件處理常式對**連接**的參數所做的變更，不會影響到**連接**。  
  
## <a name="remarks"></a>備註  
 呼叫**WillConnect**時， *ConnectionString*、 *UserID*、 *Password*和*Options*參數會設定為造成此事件之作業所建立的值（擱置連接），而且可以在事件傳回之前變更。 **WillConnect**可能會傳回暫止的連接已取消的要求。  
  
 當此事件取消時，將會呼叫**ConnectComplete** ，並將其*adStatus*參數設定為**adStatusErrorsOccurred**。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
