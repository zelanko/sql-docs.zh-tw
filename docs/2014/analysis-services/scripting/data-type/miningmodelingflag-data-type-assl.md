---
title: MiningModelingFlag 資料類型 (ASSL) |Microsoft Docs
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
- MiningModelingFlag Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelingFlag
helpviewer_keywords:
- MiningModelingFlag data type
ms.assetid: aaa72ba8-051e-4b01-b1e9-9c8d83b8b752
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ece92d63c0d66c1ef845ce2d28d3317b2f65d66f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167519"
---
# <a name="miningmodelingflag-data-type-assl"></a>MiningModelingFlag 資料類型 (ASSL)
  定義表示之可用模型旗標的基本資料型別[ModelingFlag](../objects/modelingflag-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModelingFlag>...</MiningModelingFlag>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|字串 (列舉)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|無|  
|衍生的元素|[ModelingFlag](../objects/modelingflag-element-assl.md) ([ModelingFlags](../collections/modelingflags-element-assl.md)的集合[MiningModelColumn](miningmodelcolumn-data-type-assl.md)或是[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md))|  
  
## <a name="remarks"></a>備註  
 旗標名稱可能會包含空格。 原本支援的值列於下表中。  
  
|值|描述|  
|-----------|-----------------|  
|*MODEL_EXISTENCE_ONLY*|不論資料行中的值為何，此資料行的模型應該具有兩種狀態 (遺漏或非遺漏)。 這對於巢狀資料表中的資料行 (案例之間的值很疏鬆) 特別有用。|  
|*不是 NULL*|此資料行無法接受 NULL 值。|  
|*迴歸輸入變數*|此資料行會針對測試案例提供迴歸輸入變數值。|  
  
 如果協力廠商 OLE DB 或資料採礦提供者已彙總的執行個體上可以使用其他提供者特有的旗標[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 在「分析管理物件」(AMO) 物件模型中緊密相關的元素是 <xref:Microsoft.AnalysisServices.MiningModelingFlags>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
