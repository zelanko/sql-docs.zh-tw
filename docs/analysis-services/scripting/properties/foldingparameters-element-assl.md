---
title: FoldingParameters 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- FoldIndex
- FoldCount
- MaxCases
- FoldingParameters
- FoldTargetAttribute
helpviewer_keywords:
- FoldingParameters element
ms.assetid: 5f5c5a3e-4aed-48fb-bca5-e67f421bef2f
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8d536d67738872ba070217d934a1b47be7857398
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="foldingparameters-element-assl"></a>FoldingParameters 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定當 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器執行採礦模型的交叉驗證時所用的參數。  
  
> [!NOTE]  
>  這些參數僅供內部使用。 這裡提供的資訊僅供參考。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModel>  
   ...  
   <ddl100_100:FoldingParameters>...  
      <ddl100_100:FoldIndex>...</ddl100_100:FoldIndex>  
      <ddl100_100:FoldCount>...</ddl100_100:FoldCount>  
      <ddl100_100:MaxCases>...</ddl100_100:MAxCases>  
      <ddl100_100:FoldTargetAttribute>...</ddl100_100:FoldTargetAttribute  
...</ddl100_100:FoldingParameters>  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|Description|  
|--------------------|-----------------|  
|*FoldIndex*|指示用於交叉驗證之資料分割起始位置的整數。|  
|*FoldCount*|指示交叉驗證之後在模型中之資料分割數目的整數。|  
|*MaxCases*|指示用於交叉驗證之模型案例數目的整數。<br /><br /> 0 的值表示使用所有案例。|  
|*FoldTargetAttribute*|指示包含可預測屬性之模型資料行識別碼的字串。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|子元素|*FoldIndex*<br /><br /> *FoldCount*<br /><br /> *MaxCases*<br /><br /> *FoldTargetAttribute*|  
  
## <a name="remarks"></a>備註  
 這些屬性僅供內部使用，不支援用於 DDL 陳述式。  
  
 如需有關如何使用中的交叉驗證資訊[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]，請參閱[交叉驗證報表中的量值](../../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。  
  
 如需有關如何使用執行交叉驗證資訊[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]預存程序，請參閱[資料採礦預存程序&#40;Analysis Services-Data Mining&#41;](../../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
