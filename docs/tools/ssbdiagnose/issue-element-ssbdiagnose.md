---
title: "Issue 元素 (ssbdiagnose) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssbdiagnose
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- issue element
- XML output file format [ssbdiagnose], issue element
- ssbdiagnose
ms.assetid: 2246a886-686b-44ca-9771-b155cedad8be
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb73030cc1a2788a30deea03da2892351e614d2c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="issue-element-ssbdiagnose"></a>Issue 元素 (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]找到的問題只報告**ssbdiagnose**公用程式。 **ssbdiagnose** XML 輸出檔案中每個報告的問題都有一個 Issue 元素。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Issue  
    type="..."   
    code="..."   
    server="..."   
    database="..."   
    object="...">   
    ...   
</Issue>  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|**type**|識別 Issue 元素所報告的問題類別：<br /><br /> **「診斷」** ：報告在您分析 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 設定時發現的設定問題。<br /><br /> **「問題」** ：報告讓 **ssbdiagnose** 無法完成其分析的問題。 請更正問題並重新執行 **ssbdiagnose**。<br /><br /> **「事件」** ：報告在您執行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -RUNTIME **檢查時發現的** 事件。 只有在您指定 **-SHOWEVENTS** 時才會報告事件。|  
|**代碼**|識別訊息的錯誤號碼。|  
|**伺服器**|識別在其中發現問題的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。 如果問題位於預設執行個體中，server 屬性就只有電腦名稱。 如果問題位於具名執行個體中，server 屬性就會採用 ComputerName\InstanceName 的格式。|  
|**資料庫**|識別在其中發現問題的資料庫名稱。|  
|**物件 (object)**|識別在其中發現問題的物件名稱。 如果問題是執行個體或資料庫層級問題，object 屬性就會重複執行個體或資料庫名稱。|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|**string**，沒有長度限制。|  
|**ReplTest1**|傳回錯誤訊息的文字。|  
|**出現次數**|每個報告的錯誤出現一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DiagnosticInformation 元素 &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**子元素**|無|  
  
## <a name="example"></a>範例  
 這個元素會針對沒有主要金鑰的資料庫報告 1102 錯誤，而這項錯誤是在您分析 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 組態時發現的。  
  
```  
<Issue type="Diagnosis" code="1102" server="TestComputer" database="TargetDB" object="TargetDB">The master key was not found</diagnostic>  
```  
  
## <a name="see-also"></a>請參閱  
 [ssbdiagnose 公用程式 &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
