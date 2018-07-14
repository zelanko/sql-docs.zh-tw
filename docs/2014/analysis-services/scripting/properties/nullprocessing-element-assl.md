---
title: NullProcessing 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- NullProcessing Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NullProcessing
helpviewer_keywords:
- NullProcessing element
ms.assetid: 697be5c6-e9a6-4f74-9ff4-5f31400c2178
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc55d97fabaf3f2391beb5c33e3889f6866738d4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246093"
---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*自動*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*保留*|保留 Null 值。 **注意：** 此值不支援相異計數量值。|  
|*錯誤*|引發 Null 索引鍵錯誤。 值[NullKeyNotAllowed](nullkeynotallowed-element-assl.md)判斷執行個體的錯誤回應的方式。 **注意：** 量值不支援此值。|  
|*UnknownMember*|產生未知的成員並引發 Null 轉換錯誤。 值[NullKeyConvertedToUnknown](nullkeyconvertedtounknown-element-assl.md)判斷執行個體的錯誤回應的方式。 **注意：** 量值相關聯的資料行不支援此值。|  
|*ZeroOrBlank*|將 Null 值轉換成零 (針對數值資料項目) 或空白字串 (針對字串資料項目)。 **注意︰** 這個值會提供與舊版相容性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|*自動*|使用適用於此元素的預設處理方式：<br /><br /> -   *ZeroOrBlank*針對 OLAP 資料項目。<br />-   *UnknownMember*針對資料採礦資料項目。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `NullProcessing` 允許值的列舉是 <xref:Microsoft.AnalysisServices.NullProcessing>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
