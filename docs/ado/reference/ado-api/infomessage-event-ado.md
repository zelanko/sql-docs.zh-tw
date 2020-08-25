---
description: InfoMessage 事件 (ADO)
title: InfoMessage 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
author: rothja
ms.author: jroth
ms.openlocfilehash: 4cab5acb3ccedb9a1e42426da3701bc015f0ec2d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774827"
---
# <a name="infomessage-event-ado"></a>InfoMessage 事件 (ADO)
每當**ConnectionEvent**作業期間發生警告時，就會呼叫**InfoMessage**事件。  
  
## <a name="syntax"></a>語法  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *pError*  
 [Error](./error-object.md)物件。 此參數包含任何傳回的錯誤。 如果傳回多個錯誤，則列舉 **錯誤** 集合以找出它們。  
  
 *adStatus*  
 [EventStatusEnum](./eventstatusenum.md)狀態值。 如果發生警告， *adStatus* 會設為 **AdStatusOK** ，且 *pError* 會包含警告。  
  
 在此事件傳回之前，請將此參數設定為 **adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pConnection*  
 [連接](./connection-object-ado.md)物件。 發生警告的連接。 例如，開啟**連接**物件或在**連接**上執行[命令](./command-object-ado.md)時，可能會發生警告。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](./ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../guide/data/ado-event-handler-summary.md)   
 [Connection 物件 (ADO)](./connection-object-ado.md)