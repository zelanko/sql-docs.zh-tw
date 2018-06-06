---
title: NullKeyNotAllowed 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0a7d499729efa4e9079fb01c864faf1f2a21f75d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="nullkeynotallowed-element-assl"></a>NullKeyNotAllowed 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  決定如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]處理引擎會處理在處理期間遇到 null 索引鍵錯誤。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ErrorConfiguration>  
   ...  
   <NullKeyNotAllowed>...</NullKeyNotAllowed>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*ReportAndContinue*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在不允許 Null 值的索引鍵資料行中遇到 Null 值，而強制在處理期間捨棄該記錄時，就會發生 Null 索引鍵錯誤。 不過，此錯誤時才會發生[NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md)元素**DataItem**的上階**ErrorConfiguration**父項目設定為*錯誤*。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|Value|說明|  
|-----------|-----------------|  
|*IgnoreError*|處理時忽略錯誤並繼續。|  
|*ReportAndContinue*|處理時報告錯誤並繼續。|  
|*ReportAndStop*|處理時報告錯誤並停止。|  
  
 列舉型別對應至允許的值**NullKeyNotAllowed**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ErrorOption>。  
  
## <a name="see-also"></a>另請參閱  
 [ErrorConfiguration 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)  
  
  
