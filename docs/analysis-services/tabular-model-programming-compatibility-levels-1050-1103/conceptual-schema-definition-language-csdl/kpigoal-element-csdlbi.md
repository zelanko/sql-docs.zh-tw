---
title: "KpiGoal 元素 (CSDLBI) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: fd8afbe7-b57d-4b47-862d-eb7b2489c327
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2c962ce78a66f862424ee3f4c0377cee2d0dabc0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="kpigoal-element-csdlbi"></a>KpiGoal 元素 (CSDLBI)
  KpiGoal 元素會提供資料行的參考，該資料行用來定義關鍵效能指標 (KPI) 的目標。  
  
 在 CSDLBI 中，KPI 是以量值為基礎，而且 Measure 元素會包含公式 (如果有的話)，而其他與 KPI 相關聯的中繼資料則定義為 [KPI 元素 &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md) 的一部分。  Kpigoal 元素是 Kpi 元素的子類型。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 KpiGoal 元素的屬性。  
  
|名稱|是否必要|說明|  
|----------|-----------------|-----------------|  
|PropertyRef|是|包含 KPI 目標值之資料行的參考。<br /><br /> Kpigoal 元素必須只包含單獨一個 PropertyRef 元素。<br /><br /> 請參閱 [PropertyRef 元素 &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)。|  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 CSDLBI 1.1 版中的範例顯示 Adventureworks 範本模型中的 KPI。  
  
```  
  
<Property Name="InternetCurrentSalesPerformance" Type="Double">  
  <bi:Measure>  
    <bi:Kpi StatusGraphic="Three Stars Colored">  
      <bi:KpiGoal>  
        <bi:PropertyRef Name="v_InternetCurrSalesPerf_Goal" />  
      </bi:KpiGoal>  
      <bi:KpiStatus>  
        <bi:PropertyRef Name="v_InternetCurrSalesPerf_Status" />  
      </bi:KpiStatus>  
    </bi:Kpi>  
  </bi:Measure>  
</Property>  
  
```  
  
## <a name="example"></a>範例  
 **多維度**  
  
 下列 CSDLBI 1.1 版中的範例會顯示來自 Contoso Operations Cube 的 KPI。  
  
```  
<bi:Measure   
       Caption="Sum of SalesAmount"   
       ReferenceName="Sum of SalesAmount"   
       FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
    <bi:Kpi   
       StatusGraphic="Three Circles Colored">  
      <bi:KpiGoal>  
         <bi:PropertyRef   
          Name="v_Sum_of_SalesAmount_Goal" />  
       </bi:KpiGoal>  
       <bi:KpiStatus>  
          <bi:PropertyRef   
          Name="v_Sum_of_SalesAmount_Status" />  
        </bi:KpiStatus>  
       </bi:Kpi>  
</bi:Measure>  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [KPI 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)  
  
  

