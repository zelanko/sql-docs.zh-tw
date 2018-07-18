---
title: NullProcessing 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9e5fbc3682a614dc1599347ec030348ae10bb2c0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34038362"
---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義 Null 值的處理方式。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataItem>  
   ...  
   <NullProcessing>...</NullProcessing>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*Automatic*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*保留*|保留 Null 值。<br /><br /> 注意： 此值不支援相異計數量值。|  
|*錯誤*|引發 Null 索引鍵錯誤。 值[NullKeyNotAllowed](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md)判斷執行個體的錯誤回應的方式。<br /><br /> 注意： 此值不支援量值。|  
|*UnknownMember*|產生未知的成員並引發 Null 轉換錯誤。 值[NullKeyConvertedToUnknown](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md)判斷執行個體的錯誤回應的方式。<br /><br /> 注意： 此值不支援量值相關聯的資料行。|  
|*ZeroOrBlank*|將 Null 值轉換成零 (針對數值資料項目) 或空白字串 (針對字串資料項目)。<br /><br /> 注意： 這個值會提供與舊版的相容性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|*Automatic*|使用適用於此元素的預設處理方式：<br /><br /> *ZeroOrBlank* (針對 OLAP 資料項目)。<br /><br /> *UnknownMember* (針對資料採礦資料項目)。|  
  
 列舉型別對應至允許的值**NullProcessing**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.NullProcessing>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
