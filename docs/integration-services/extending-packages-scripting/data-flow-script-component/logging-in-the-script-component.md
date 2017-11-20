---
title: "登入指令碼元件 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 410a2472399574753d67a44b93437b1698c8b086
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="logging-in-the-script-component"></a>在指令碼元件中記錄
  在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 封裝中記錄可以讓您藉由記錄預先定義之事件或使用者定義訊息，記錄關於執行進度、結果和問題的詳細資訊以供稍後分析。 指令碼元件可以使用<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>方法**ScriptMain**類別來記錄使用者定義的資料。 如果已啟用記錄，而**ScriptComponentLogEntry**的登入選取的事件**詳細資料** 索引標籤**設定 SSIS 記錄**對話方塊中，呼叫一次<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>方法將事件資訊儲存在所有已設定的資料流程工作的記錄提供者。  
  
 以下是記錄的一個簡單範例：  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  雖然您可以直接從指令碼元件執行記錄，不過您可能會想要考慮實作事件，而不是記錄。 使用事件時，不僅可以啟用事件訊息的記錄，還可用預設或使用者定義的事件處理常式回應事件。  
  
 如需記錄的詳細資訊，請參閱[Integration Services &#40;SSIS &#41;記錄](../../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS &#41;記錄](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  

