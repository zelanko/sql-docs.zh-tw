---
title: "DiagnosticInformation 元素 (ssbdiagnose) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
ms.assetid: 0cfda544-542c-4cf4-86d2-8031c91b10f6
caps.latest.revision: "14"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82593d8330e5f7263ff43c6b408998164425617f
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>DiagnosticInformation 元素 (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]**DiagnosticInformation**元素包含報告此公用程式所找到的診斷資訊的所有元素。 **DiagnosticInformation** 是 **ssbdiagnostic** XML 輸出檔的根元素。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DiagnosticInformation>   
    ...   
</DiagnosticInformation>  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|Attribute|Description|  
|---------------|-----------------|  
|**無**|해당 사항 없음|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個 **ssbdiagnose** XML 輸出檔發生一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|無。|  
|**子元素**|[Banner 元素 &#40; ssbdiagnose&#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)<br /><br /> [Issue 元素 &#40; ssbdiagnose&#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)|  
  
## <a name="remarks"></a>備註  
 如需有關 XML 命名空間的詳細資訊，請參閱 [MSDN Library 中的＜](http://go.microsoft.com/fwlink/?LinkId=7341) XML 文件中的命名空間 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ＞(英文)。  
  
## <a name="see-also"></a>另請參閱  
 [ssbdiagnose 公用程式 &#40;Service Broker &#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
