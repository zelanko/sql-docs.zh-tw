---
description: Cancel 方法 (RDS)
title: " (RDS) 的 Cancel 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
author: rothja
ms.author: jroth
ms.openlocfilehash: ade9d0092a5dbc0ebdaba0ae968d52b23c97ba27
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982779"
---
# <a name="cancel-method-rds"></a>Cancel 方法 (RDS)
取消執行暫止的非同步方法呼叫。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
RDS.DataControl.Cancel  
```  
  
## <a name="remarks"></a>備註  
 當您呼叫 **Cancel**時， [ReadyState](./readystate-property-rds.md) 會自動設定為 **adcReadyStateLoaded**，而且 [記錄集](../ado-api/recordset-object-ado.md) 將會是空的。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Cancel 方法範例 (VBScript) ](./cancel-method-example-vbscript.md)   
 [ (ADO) 的 Cancel 方法 ](../ado-api/cancel-method-ado.md)   
 [ (ADO) 的 CancelBatch 方法 ](../ado-api/cancelbatch-method-ado.md)   
 [ (ADO) 的 CancelUpdate 方法 ](../ado-api/cancelupdate-method-ado.md)   
 [RDS)  (CancelUpdate 方法 ](./cancelupdate-method-rds.md)   
 [ExecuteOptions 屬性 (RDS)](./executeoptions-property-rds.md)