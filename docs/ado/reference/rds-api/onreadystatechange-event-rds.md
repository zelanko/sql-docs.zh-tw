---
description: onReadyStateChange 事件 (RDS)
title: onReadyStateChange (RDS) 的事件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
author: rothja
ms.author: jroth
ms.openlocfilehash: ee9f48a3cba1190cdd9400b5ee5ecb30c35bfaed
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724449"
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange 事件 (RDS)
每當[ReadyState](./readystate-property-rds.md)屬性的值變更時，就會呼叫**onReadyStateChange**事件。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="syntax"></a>語法  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>參數  
 無。  
  
## <a name="remarks"></a>備註  
 **ReadyState**屬性會反映 RDS 的進度[。DataControl](./datacontrol-object-rds.md)物件，它會以非同步方式將資料取出至其[記錄集](../ado-api/recordset-object-ado.md)物件。 使用 **onReadyStateChange** 事件可在 **ReadyState** 屬性發生時監視其變更。 這比定期檢查屬性的值更有效率。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](../ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../guide/data/ado-event-handler-summary.md)