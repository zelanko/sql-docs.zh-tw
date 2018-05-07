---
title: ReportAction 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb74ce436b7c10882f6ccad822684e782066f636
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="reportaction-data-type-assl"></a>ReportAction 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義代表產生動作的衍生的資料類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]報表。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ReportAction>  
   <!-- The following elements extend Action -->  
   <ReportServer>...</ReportServer>  
   <Path>...</Path>  
   <ReportParameters>...</ReportParameters>  
   <ReportFormatParameters>...</ReportFormatParameters>  
</ReportAction>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[動作](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[路徑](../../../analysis-services/scripting/properties/path-element-assl.md)， [ReportFormatParameters](../../../analysis-services/scripting/collections/reportformatparameters-element-assl.md)， [ReportParameters](../../../analysis-services/scripting/collections/reportparameters-element-assl.md)， [ReportServer](../../../analysis-services/scripting/properties/reportserver-element-assl.md)|  
|衍生的元素|[動作](../../../analysis-services/scripting/objects/action-element-assl.md)([動作](../../../analysis-services/scripting/collections/actions-element-assl.md)集合[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)或[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 報表伺服器會回應以 URL 為基礎的報表要求。 報表動作定義為型別*報表*。 建立此動作時，系統會將資源和參數傳送到伺服器。 伺服器會將此動作公開成為類型資料列集的動作。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ReportAction>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
