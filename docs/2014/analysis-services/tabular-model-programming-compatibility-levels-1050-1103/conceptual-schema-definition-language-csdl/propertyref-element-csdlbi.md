---
title: PropertyRef 元素 (CSDLBI) |Microsoft 文件
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
ms.assetid: 8299efb9-e224-4a82-bdfc-a74ec92f8711
caps.latest.revision: 4
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 1b4d64cc0e0e59029361412bc96bd98559be51b4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133326"
---
# <a name="propertyref-element-csdlbi"></a>PropertyRef 元素 (CSDLBI)
  PropertyRef 元素是簡單類型，可提供為另一個屬性提供所需值的資料行參考。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 PropertyRef 元素的元素和屬性。  
  
|[屬性]|是否必要|描述|  
|----------|-----------------|-----------------|  
|[屬性]|是|字串，包含做為參考目標之屬性的名稱。|  
  
## <a name="propertyrefs-element"></a>PropertyRefs 元素  
 PropertyRefs 是複雜類型，用於定義屬性集合，其中每個屬性都包含在 PropertyRef 元素中。  
  
 下表列出 PropertyRefs 類型的元素和屬性。  
  
|[屬性]|是否必要|描述|  
|----------|-----------------|-----------------|  
|PropertyRef|是|包含屬性參考的字串。|  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 CSDLBI 1.1 版中的範例顯示 PropertyRef 元素，它會根據 AdventureWorks 表格式模型範例指定量值中使用的公式來源。  
  
```  
<bi:Measure Caption="Total Current Quarter Margin Performance" ReferenceName="Total Current Quarter Margin Performance" Width="0" IsSimpleMeasure="false">  
  <bi:Kpi StatusGraphic="Three Symbols UnCircled Colored">  
    <bi:KpiGoal>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Goal_" />  
    </bi:KpiGoal>  
    <bi:KpiStatus>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Status_" />  
    </bi:KpiStatus>  
  </bi:Kpi>  
</bi:Measure>  
```  
  
## <a name="example"></a>範例  
 **多維度**  
  
 下列 CSDLBI 1.1 版中的範例會顯示來自 Contoso Operations Cube 的 KPI。 PropertyRef 元素會指向資料行，這些資料行包含用於定義 KPI 的目標和相對於該目標之狀態的公式或值。  
  
```  
<Property Name="Sum_of_SalesAmount" Type="Decimal" Precision="19" Scale="4">  
   <Documentation>  
     <Summary>KPI Description</Summary>  
   </Documentation>  
     <bi:Measure   
         Caption="Sum of SalesAmount"   
         ReferenceName="Sum of SalesAmount"   
         FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
     <bi:Kpi   
           StatusGraphic="Three Circles Colored">  
         <bi:KpiGoal>  
            <bi:PropertyRef Name="v_Sum_of_SalesAmount_Goal" />  
          </bi:KpiGoal>  
          <bi:KpiStatus>  
              <bi:PropertyRef Name="v_Sum_of_SalesAmount_Status" />  
          </bi:KpiStatus>  
     </bi:Kpi>  
     </bi:Measure>  
</Property>  
```  
  
## <a name="see-also"></a>另請參閱  
 [CSDL 之 BI 註解的技術參考](technical-reference-for-bi-annotations-to-csdl.md)  
  
  