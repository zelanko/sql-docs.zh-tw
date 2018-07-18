---
title: Hierarchy 元素 (CSDLBI) |Microsoft Docs
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
ms.assetid: 9debb638-1b28-401b-9499-8f63943863e9
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: be67c3059f09beefae68d0264fd0316579344d64
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250788"
---
# <a name="hierarchy-element-csdlbi"></a>Hierarchy 元素 (CSDLBI)
  Hierarchy 元素是資料表中可彼此連結以構成階層之欄位的邏輯容器。 Hierarchy 元素衍生自 CSDL Member 元素而且已擴充，可支援商業智慧資料模型中建立的階層。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 Hierarchy 元素的元素和屬性  
  
|名稱|是否必要|描述|  
|----------|-----------------|-----------------|  
|文件集|否|階層的描述。|  
|層級|是|一個或多個 Level 元素，會定義階層中所使用的資料行。<br /><br /> 請參閱 [Level 元素 &#40;CSDLBI&#41;](level-element-csdlbi.md)。|  
  
## <a name="remarks"></a>備註  
 在表格式模型中，您可以在相同資料表的資料行之間指定父子式關聯性，藉以建立階層。 如需詳細資訊，請參閱[階層 &#40;SSAS 表格式&#41;](../../tabular-models/hierarchies-ssas-tabular.md)。  
  
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
 [了解表格式物件模型](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [了解 DAX 中父子式階層的函數](https://msdn.microsoft.com/library/gg492192(v=sql.120).aspx)   
 [設定&#40;所有&#41;屬性階層的層級](../../multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
