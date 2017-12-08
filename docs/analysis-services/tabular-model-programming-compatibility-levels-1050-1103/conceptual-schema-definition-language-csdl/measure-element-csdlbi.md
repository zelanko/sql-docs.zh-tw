---
title: "量值元素 (CSDLBI) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: bfbc9274-053a-421a-bb81-2095bba710be
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 83dc8a37899d510205659b9a017dd6246c9ca695
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="measure-element-csdlbi"></a>Measure 元素 (CSDLBI)
  Measure 元素是以 CSDL Property 元素為基礎的複雜類型。 CSDLBI 註解會加入支援複雜公式定義的屬性，以便在商業智慧資料模型中使用。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 Measure 元素的元素和屬性，以及適用於 Property 元素的所有屬性。  
  
|名稱|是否必要|說明|  
|----------|-----------------|-----------------|  
|Kpi|否|僅為做為 KPI 使用的量值所需。 並非所有量值都是 KPI，但是所有 KPI 都必須以量值的定義為基礎。<br /><br /> [KPI 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)|  
|IsSimpleMeasure|否|True/false 值，指出用於量值的公式是否為其中一個簡單彙總 (SUM、COUNT、MIN、MAX、AVG、DistinctCount)。<br /><br /> 預設為 true。|  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 CSDLBI 1.1 版的範例會顯示 AdventureWorks 表格式模型範例中的兩個量值。 第二個量值已經透過加入 KPI 元素，轉換成 KPI。  
  
```  
  
<Property   
    Name="Order_Lines_Count"   
    Type="Int64">  
<bi:Measure   
    Caption="Order Lines Count"   
    ReferenceName="Order Lines Count"   
    Width="0"   
    IsSimpleMeasure="false" />  
</Property>  
  
<Property   
    Name="Total_Current_Quarter_Sales_Performance"   
    Type="Double">  
<bi:Measure   
    Caption="Total Current Quarter Sales Performance"   
    ReferenceName="Total Current Quarter Sales Performance"   
    Width="0"   
    IsSimpleMeasure="false">  
    <bi:Kpi   
    StatusGraphic="Three Signs Colored">  
      <bi:KpiGoal>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Goal_" />  
      </bi:KpiGoal>  
      <bi:KpiStatus>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Status_" />  
      </bi:KpiStatus>  
    </bi:Kpi>  
  </bi:Measure>  
</Property>  
```  
  
## <a name="example"></a>範例  
 **Multidimensiona;**  
  
 下列 CSDLBI 1.1 版中的範例會顯示 Contoso Operations Cube 中要做為 KPI 使用的量值。  
  
```  
  
<Property   
    Name="Sum_of_SalesAmount"   
    Type="Decimal" Precision="19" Scale="4">  
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
  
## <a name="see-also"></a>請參閱＜  
 [CSDL 之 BI 註解的技術參考](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
