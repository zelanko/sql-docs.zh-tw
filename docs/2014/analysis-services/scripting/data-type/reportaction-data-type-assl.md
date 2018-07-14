---
title: ReportAction 資料類型 (ASSL) |Microsoft Docs
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
- ReportAction Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportAction
helpviewer_keywords:
- ReportAction data type
ms.assetid: b22f0d52-ed3a-4239-840e-0eaf172d7276
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bacb34e6a57126048253a5292fe19627838d21e1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176395"
---
# <a name="reportaction-data-type-assl"></a>ReportAction 資料類型 (ASSL)
  定義代表產生的動作的衍生的資料類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]報表。  
  
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
|基底資料類型|[動作](action-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[路徑](../properties/path-element-assl.md)， [ReportFormatParameters](../collections/reportformatparameters-element-assl.md)， [ReportParameters](../collections/reportparameters-element-assl.md)， [ReportServer](../objects/server-element-assl.md)|  
|衍生的元素|[動作](../objects/action-element-assl.md)([動作](../collections/actions-element-assl.md)的集合[Cube](../objects/cube-element-assl.md)或是[觀點來看](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 報表伺服器會回應以 URL 為基礎的報表要求。 報表動作定義為型別*報表*。 建立此動作時，系統會將資源和參數傳送到伺服器。 伺服器會將此動作公開成為類型資料列集的動作。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.ReportAction>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
