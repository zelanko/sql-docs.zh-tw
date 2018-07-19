---
title: DimensionPermission 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f0057a29a6af37dbecbe87bc777237bc6c7ecdd
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029269"
---
# <a name="dimensionpermission-data-type-assl"></a>DimensionPermission 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[AttributePermissions](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)， [AllowedRowsExpression](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)|  
|衍生的元素|[DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 此元素在 DeploymentMode 值 2 (表格式伺服器模式) 下，擁有下列驗證。  
  
-   *AttributePermission*屬性必須是空的或發生錯誤。  
  
 此元素在 DeploymentMode 值 0 (OLAP) 下，擁有下列驗證。  
  
-   *AllowedRowsExpression*屬性必須是空的或發生錯誤。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DimensionPermission>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
