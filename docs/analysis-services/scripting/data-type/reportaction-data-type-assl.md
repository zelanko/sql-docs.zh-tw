---
title: ReportAction 資料類型 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ReportAction Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ReportAction
helpviewer_keywords:
- ReportAction data type
ms.assetid: b22f0d52-ed3a-4239-840e-0eaf172d7276
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e8103a26b28517d7db2550830811915a874b46b4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="reportaction-data-type-assl"></a>ReportAction 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義代表產生動作的衍生的資料類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]報表。  
  
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
  
|特性|描述|  
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
  
## <a name="see-also"></a>請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
