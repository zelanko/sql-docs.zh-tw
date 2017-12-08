---
title: "ImpersonationInfo 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ImpersonationInfo Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: ImpersonationInfo element
ms.assetid: d4b9c372-1023-43f7-97e9-b0a90f544fbb
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 91bc024cd8d42bc77f4df1b431d4df25c053a133
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="impersonationinfo-element-assl"></a>ImpersonationInfo 元素 (ASSL)
  包含在存取或執行組件時，用來決定模擬行為的資訊。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Assembly> <!-- or one of the elements listed in the Element Relationships table -->  
   <ImpersonationInfo>  
      <!-- Child elements are only those that are inherited from ImpersonationInfo -->  
   </ImpersonationInfo>  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[組件](../../../analysis-services/scripting/data-type/assembly-data-type-assl.md)，[資料來源](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>請參閱＜  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
