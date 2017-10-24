---
title: "DiagnosticInformation 元素 (ssbdiagnose) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
ms.assetid: 0cfda544-542c-4cf4-86d2-8031c91b10f6
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9d5a21ac18d6b4982c7c93bf11e3bf16051dc0c7
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>DiagnosticInformation 元素 (ssbdiagnose)
  **DiagnosticInformation** 元素包含報告此公用程式找到之診斷資訊的所有元素。 **DiagnosticInformation** 是 **ssbdiagnostic** XML 輸出檔的根元素。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DiagnosticInformation>   
    ...   
</DiagnosticInformation>  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|Attribute|描述|  
|---------------|-----------------|  
|**無**|不適用|  
  
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
  
  

