---
title: KeyDuplicate 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- KeyDuplicate Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KeyDuplicate
helpviewer_keywords:
- KeyDuplicate element
ms.assetid: d7000b8b-e81f-4401-8738-00c2e0f73a59
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6bbd445a1b362e7ae5bc7c12df3404efe1a781ea
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192440"
---
# <a name="keyduplicate-element-assl"></a>KeyDuplicate 元素 (ASSL)
  決定如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]處理在處理期間遇到重複的索引鍵錯誤。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyDuplicate>...</KeyDuplicate>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*IgnoreError*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 只有在進行維度處理期間，屬性索引鍵出現一次以上才會產生重複索引鍵錯誤。 由於屬性索引鍵必須是唯一的，所以 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會捨棄重複的記錄。 重複索引鍵錯誤通常代表維度的設計 (特別是屬性之間的關聯性) 中含有缺陷。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*IgnoreError*|處理時應該忽略錯誤並繼續。|  
|*ReportAndContinue*|處理時應該報告錯誤並繼續。|  
|*ReportAndStop*|處理時應該報告錯誤並停止。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `KeyDuplicate` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ErrorOption>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
