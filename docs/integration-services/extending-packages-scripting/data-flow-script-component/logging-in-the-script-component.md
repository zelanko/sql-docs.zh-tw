---
title: 在指令碼元件中記錄 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9a45bb6728637d087063d4e90c51734396e98c06
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785906"
---
# <a name="logging-in-the-script-component"></a>在指令碼元件中記錄
  在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 封裝中記錄可以讓您藉由記錄預先定義之事件或使用者定義訊息，記錄關於執行進度、結果和問題的詳細資訊以供稍後分析。 指令碼元件可以使用 **ScriptMain** 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法記錄使用者定義的資料。 如果已啟用記錄，而且已在 [設定 SSIS 記錄] 對話方塊的 [詳細資料] 索引標籤上選取 **ScriptComponentLogEntry** 事件以進行記錄，<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法的單一呼叫會儲存為資料流程工作設定之所有記錄提供者中的事件資訊。  
  
 以下是記錄的一個簡單範例：  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  雖然您可以直接從指令碼元件執行記錄，不過您可能會想要考慮實作事件，而不是記錄。 使用事件時，不僅可以啟用事件訊息的記錄，還可用預設或使用者定義的事件處理常式回應事件。  
  
 如需記錄的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 記錄](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
