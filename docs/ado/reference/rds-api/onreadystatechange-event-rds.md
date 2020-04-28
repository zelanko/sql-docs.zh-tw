---
title: onReadyStateChange 事件（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3558fc1fecd343fff480cca3b45c468860a801f8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963832"
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange 事件 (RDS)
每當[ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)屬性的值變更時，就會呼叫**onReadyStateChange**事件。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>參數  
 無。  
  
## <a name="remarks"></a>備註  
 **ReadyState**屬性會反映 RDS 的進度[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件，因為它會以非同步方式將資料捕獲到其[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 每當發生**ReadyState**屬性時，請使用**onReadyStateChange**事件來監視變更。 這比定期檢查屬性的值更有效率。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)


