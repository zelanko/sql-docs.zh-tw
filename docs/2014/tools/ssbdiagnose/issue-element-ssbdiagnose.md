---
title: Issue 元素 (ssbdiagnose) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- issue element
- XML output file format [ssbdiagnose], issue element
- ssbdiagnose
ms.assetid: 2246a886-686b-44ca-9771-b155cedad8be
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: adff003b1d6b98d7778311b84aca4666dd802d27
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134522"
---
# <a name="issue-element-ssbdiagnose"></a>Issue 元素 (ssbdiagnose)
  報告 **ssbdiagnose** 公用程式所發現的問題。 **ssbdiagnose** XML 輸出檔案中每個報告的問題都有一個 Issue 元素。  
  
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
|`type`|識別 Issue 元素所報告的問題類別：<br /><br /> **「診斷」** ：報告在您分析 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 設定時發現的設定問題。<br /><br /> **「問題」** ：報告讓 **ssbdiagnose** 無法完成其分析的問題。 請更正問題並重新執行 **ssbdiagnose**。<br /><br /> **「事件」** ：報告在您執行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -RUNTIME **檢查時發現的** 事件。 只有在您指定 **-SHOWEVENTS** 時才會報告事件。|  
|`code`|識別訊息的錯誤號碼。|  
|`server`|識別在其中發現問題的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。 如果問題位於預設執行個體中，server 屬性就只有電腦名稱。 如果問題位於具名執行個體中，server 屬性就會採用 ComputerName\InstanceName 的格式。|  
|`database`|識別在其中發現問題的資料庫名稱。|  
|`object`|識別在其中發現問題的物件名稱。 如果問題是執行個體或資料庫層級問題，object 屬性就會重複執行個體或資料庫名稱。|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|`string`長度沒有限制。|  
|**ReplTest1**|傳回錯誤訊息的文字。|  
|**出現次數**|每個報告的錯誤出現一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DiagnosticInformation 元素&#40;ssbdiagnose&#41;](diagnosticinformation-element-ssbdiagnose.md)|  
|**子元素**|無|  
  
## <a name="example"></a>範例  
 這個元素會針對沒有主要金鑰的資料庫報告 1102 錯誤，而這項錯誤是在您分析 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 組態時發現的。  
  
```  
<Issue type="Diagnosis" code="1102" server="TestComputer" database="TargetDB" object="TargetDB">The master key was not found</diagnostic>  
```  
  
## <a name="see-also"></a>另請參閱  
 [ssbdiagnose 公用程式 &#40;Service Broker&#41;](ssbdiagnose-utility-service-broker.md)  
  
  