---
description: onError 事件 (RDS)
title: onError 事件 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onError event [ADO]
ms.assetid: b01cbc62-fbd7-4068-b16c-8b0f80a05887
author: rothja
ms.author: jroth
ms.openlocfilehash: 56caf584d45b76315ff95cf6001a2ce1c882f579
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724459"
---
# <a name="onerror-event-rds"></a>onError 事件 (RDS)
每當作業期間發生錯誤時，就會呼叫 **onError** 事件。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="syntax"></a>語法  
  
```  
  
onError SCode, Description, Source, CancelDisplay  
```  
  
#### <a name="parameters"></a>參數  
 *SCode*  
 整數，表示錯誤的狀態碼。  
  
 *描述*  
 表示錯誤描述的 **字串** 。  
  
 *Source*  
 **字串**，指出造成錯誤的查詢或命令。  
  
 *CancelDisplay*  
 **布林**值，如果設定為**True**，則會防止錯誤顯示在對話方塊中。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](../ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../guide/data/ado-event-handler-summary.md)