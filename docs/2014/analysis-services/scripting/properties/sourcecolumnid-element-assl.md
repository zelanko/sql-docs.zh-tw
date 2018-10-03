---
title: SourceColumnID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- SourceColumnID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SourceColumnID
helpviewer_keywords:
- SourceColumnID element
ms.assetid: 715c0be7-aa07-4dff-a909-9738224941ec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f4bfcf8969123515436be0d53b181747c322b110
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187898"
---
# <a name="sourcecolumnid-element-assl"></a>SourceColumnID 元素 (ASSL)
  包含上階中來源採礦結構資料行的識別碼 (ID) [MiningStructure](../objects/miningstructure-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <SourceColumnID>...</SourceColumnID>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 值`SourceColumnID`項目符合識別項中的採礦結構資料行[資料行](../collections/columns-element-assl.md)集合之父代`MiningStructure`。  
  
 對應至父系的元素`SourceColumnID`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.MiningModelColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
