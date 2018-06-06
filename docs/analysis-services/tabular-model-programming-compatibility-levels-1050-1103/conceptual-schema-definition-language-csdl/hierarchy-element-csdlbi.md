---
title: Hierarchy 元素 (CSDLBI) |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 99884f036225b8070e8c78f03836fa1c48b2f9c6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="hierarchy-element-csdlbi"></a>Hierarchy 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Hierarchy 元素是資料表中可彼此連結以構成階層之欄位的邏輯容器。 Hierarchy 元素衍生自 CSDL Member 元素而且已擴充，可支援商業智慧資料模型中建立的階層。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 Hierarchy 元素的元素和屬性  
  
|名稱|是否必要|說明|  
|----------|-----------------|-----------------|  
|文件集|否|階層的描述。|  
|Level|是|一個或多個 Level 元素，會定義階層中所使用的資料行。<br /><br /> 請參閱 [Level 元素 &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/level-element-csdlbi.md)。|  
  
## <a name="remarks"></a>備註  
 在表格式模型中，您可以在相同資料表的資料行之間指定父子式關聯性，藉以建立階層。 如需詳細資訊，請參閱[階層](../../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)。  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 CSDLBI 1.0 版中的範例顯示 AdventureWorks 範本模型中已加入 Products 資料表的階層。  
  
```  
  
<bi:Hierarchy Name="Categoryy">  
    <bi:Level Name="CategoryName">  
       <bi:Source>  
       <bi:PropertyRef Name="CategoryName" />  
       </bi:Source>  
    </bi:Level>  
    <bi:Level Name="ProductName">  
       <bi:Source>  
       <bi:PropertyRef Name="ProductName" />  
       </bi:Source>  
    </bi:Level>  
</bi:Hierarchy>  
  
```  
  
## <a name="example"></a>範例  
 **多維度**  
  
 下列 CSDLBI 1.1 版中的範例會顯示來自 Contoso Retail Operations Cube 的階層。  
  
```  
  
<bi:Hierarchy Name="Product_Hierarchy" Caption="Product Hierarchy" ReferenceName="Product Hierarchy">  
   <bi:Documentation>  
      <bi:Summary>DESCRIPTION_ProductModelCateg_Hierarchies</bi:Summary>  
   </bi:Documentation>  
  
   <bi:Level Name="ProductLine">  
      <bi:Source>  
      <bi:PropertyRef Name="ProductLine" />  
      </bi:Source>  
   </bi:Level>  
  
   <bi:Level Name="ModelName">  
         <bi:Source>  
      <bi:PropertyRef Name="ModelName" />  
      </bi:Source>  
   </bi:Level>  
</bi:Hierarchy>  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [了解表格式物件模型在相容性層級 1050年透過 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [了解 DAX 中的父子式階層的函數](http://msdn.microsoft.com/en-us/b11f0cff-cee4-4ae7-a5b3-ebe288fc42d3)   
 [設定 & #40;所有 & #41;屬性階層層級](../../../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
