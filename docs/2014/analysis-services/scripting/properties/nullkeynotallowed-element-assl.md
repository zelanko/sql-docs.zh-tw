---
title: NullKeyNotAllowed 元素 (ASSL) |Microsoft 文件
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
- NullKeyNotAllowed Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NullKeyNotAllowed
helpviewer_keywords:
- NullKeyNotAllowed element
ms.assetid: 4ece99eb-954b-4da1-add4-dd9efd5fff0a
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 235c76fb2b8cad1682fab97f36cb1867d7c82c38
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023201"
---
# <a name="nullkeynotallowed-element-assl"></a>NullKeyNotAllowed 元素 (ASSL)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*ReportAndContinue*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在不允許 Null 值的索引鍵資料行中遇到 Null 值，而強制在處理期間捨棄該記錄時，就會發生 Null 索引鍵錯誤。 不過，此錯誤時才會發生[NullProcessing](nullprocessing-element-assl.md)元素`DataItem`的上階`ErrorConfiguration`父項目設定為*錯誤*。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*IgnoreError*|處理時忽略錯誤並繼續。|  
|*ReportAndContinue*|處理時報告錯誤並繼續。|  
|*ReportAndStop*|處理時報告錯誤並停止。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `NullKeyNotAllowed` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ErrorOption>。  
  
## <a name="see-also"></a>另請參閱  
 [ErrorConfiguration 元素&#40;ASSL&#41;](../objects/errorconfiguration-element-assl.md)  
  
  