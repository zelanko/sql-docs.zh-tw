---
title: DimensionPermission 資料類型 (ASSL) |Microsoft 文件
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
- DimensionPermission Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DimensionPermission data type
ms.assetid: 066405ff-903f-467a-b0d5-e58653952c52
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1c614d2fd30f7bd3b831c571cc4d3de0cf26e365
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035077"
---
# <a name="dimensionpermission-data-type-assl"></a>DimensionPermission 資料類型 (ASSL)
  定義代表指派給資料庫維度之權限的衍生資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionPermission>  
   <!-- The following elements extend Permission -->  
   <AttributePermissions>...</AttributePermissions>  
   <AllowedRowsExpression>...</AllowedRowsExpression>  
</DimensionPermission>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[權限](permission-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[AttributePermissions](../collections/attributepermissions-element-assl.md)， [AllowedRowsExpression](../collections/attributepermissions-element-assl.md)|  
|衍生的元素|[DimensionPermission](../objects/dimensionpermission-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 此元素在 DeploymentMode 值 2 (表格式伺服器模式) 下，擁有下列驗證。  
  
-   *AttributePermission*屬性必須是空的或發生錯誤。  
  
 此元素在 DeploymentMode 值 0 (OLAP) 下，擁有下列驗證。  
  
-   *AllowedRowsExpression*屬性必須是空的或發生錯誤。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DimensionPermission>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  