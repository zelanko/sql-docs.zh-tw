---
title: KeyErrorAction 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5bbc6bdac0fe57d2ad585fd9bb9d10c4c8dd4692
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34034899"
---
# <a name="keyerroraction-element-assl"></a>KeyErrorAction 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定的動作[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]才會發生錯誤時在索引鍵。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyErrorAction>...</KeyErrorAction>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*ConvertToUnknown*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|說明|  
|-----------|-----------------|  
|*ConvertToUnknown*|將問題索引鍵轉換成未知成員值。|  
|*DiscardRecord*|捨棄記錄。|  
  
 列舉型別對應至允許的值**KeyErrorAction**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.KeyErrorAction>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
