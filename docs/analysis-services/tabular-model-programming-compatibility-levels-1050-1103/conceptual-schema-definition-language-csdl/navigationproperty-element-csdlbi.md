---
title: NavigationProperty 元素 (CSDLBI) |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 769e0e59ffe276d606188d7ac432b7e16205607c
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2018
---
# <a name="navigationproperty-element-csdlbi"></a>NavigationProperty 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  NavigationProperty 元素是複雜類型，它會擴充 CSDL Member 類型，以支援在商業智慧資料模型中導覽。  
  
> [!WARNING]  
>  此元素適用於報告，無法加以修改或操作。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 NavigationProperty 元素的元素和屬性。  
  
|名稱|是否必要|說明|  
|----------|-----------------|-----------------|  
|CollectionCaption|否|複數名稱，用於參考導覽屬性的一組執行個體。<br /><br /> 如果省略此屬性，則會使用基底 Member 的 Caption 屬性。|  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列範例顯示 CSDLBI 1.1 版的導覽屬性，其中描述表格式模型中的 Product SubCategory 資料表與 Product 資料表之間的連結。  
  
```  
  
<NavigationProperty   
    Name="Product_Sub_Category_ProductSubcategoryKey"      
    Relationship="Sandbox.Product_Product_Sub_Category_Product_Sub_Category_ProductSubcategoryKey"  
     FromRole="Product_ProductSubcategoryKey"   
    ToRole="Product_Sub_Category_ProductSubcategoryKey">  
<bi:NavigationProperty   
     ReferenceName="Product Sub-Category_ProductSubcategoryKey" />  
</NavigationProperty>  
```  
  
## <a name="example"></a>範例  
 **多維度**  
  
 下列範例顯示 CSDLBI 1.1 版的導覽屬性，其中描述 Contoso Operations Cube 中兩個資料表之間的關聯性。 此關聯性連接 Bike Category 資料表與 Product Subcategory 資料表。  
  
```  
  
<NavigationProperty   
     Name="BikeSubcategory_ProductSubcategoryKey"   
     Relationship="Sandbox.Bike_BikeSubcategory_BikeSubcategory_ProductSubcategoryKey"   
     FromRole="Bike_ProductSubcategoryKey"   
     ToRole="BikeSubcategory_ProductSubcategoryKey">  
   <bi:NavigationProperty />  
</NavigationProperty>  
```  
  
## <a name="see-also"></a>另請參閱  
 [了解表格式物件模型在相容性層級 1050年透過 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
