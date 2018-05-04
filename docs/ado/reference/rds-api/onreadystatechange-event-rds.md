---
title: onReadyStateChange 事件 (RDS) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 194fcfd86f7e254a271bcf8785354a3dbc82c151
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange 事件 (RDS)
**OnReadyStateChange**事件被呼叫時的值[ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)屬性變更。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>參數  
 無。  
  
## <a name="remarks"></a>備註  
 **ReadyState**屬性會反映的進度[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件，因為它會以非同步方式擷取資料到其[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 使用**onReadyStateChange**事件監視中的變更**ReadyState**時出現的屬性。 這是比定期檢查屬性的值更有效率。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)


