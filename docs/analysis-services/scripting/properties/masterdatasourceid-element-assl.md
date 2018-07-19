---
title: MasterDatasourceID 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0d15ac7183d703b0c02ffa1de5b5993810bd77b8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34033249"
---
# <a name="masterdatasourceid-element-assl"></a>MasterDatasourceID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含主要資料來源識別碼 (ID)[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Database>  
   ...  
   <MasterDatasourceID>...</MasterDatasourceID>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 遠端執行個體上資料庫[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ，包含遠端資料分割， **MasterDatasourceID**項目包含用來識別主要資料來源識別碼的資料來源執行個體[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]管理遠端資料分割。  
  
 對應目的父代的項目**MasterDatasourceID**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Database>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
