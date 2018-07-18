---
title: KPI 元素 (CSDLBI) |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bc368aed1186c20e76ce643a33673030713547ba
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34041329"
---
# <a name="kpi-element-csdlbi"></a>KPI 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Kpi 元素會定義可當做關鍵效能指標 (KPI) 使用的計算。 在商業智慧資料模型中，KPI 是以量值為基礎，因此 KPI 的定義會包含與量值關聯的所有中繼資料以及呈現 KPI 值所需的資訊，包括預設圖形。  
  
 Kpi 元素不會指定包含在量值定義中的公式，而是指定與當做 KPI 使用之量值相關聯的其他中繼資料。 一旦您將量值指定為 KPI 之後，就無法將它當做量值用於其他內容。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 Kpi 元素的元素和屬性。  
  
|名稱|是否必要|說明|  
|----------|-----------------|-----------------|  
|文件集|否|KPI 的描述。|  
|KpiGoal|是|資料行的參考，其中包含可用來做為目標的值。<br /><br /> 請參閱 [PropertyRef 元素 &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)。|  
|KpiStatus|是|資料行的參考，其中包含代表 KPI 目前狀態的值。|  
|StatusGraphic|是|針對 KPI 中定義的目標指出負面、中性或正面進度之影像的參考。|  
  
## <a name="remarks"></a>備註  
 當您設計模型時，可以建立量值，然後指派要當做 KPI 使用的量值，藉以建立 KPI。 接著，您可以加入 KPI 特有的資訊，例如要用於顯示趨勢的圖形。  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 CSDLBI 1.0 版的範例會根據 AdventureWorks 表格式模型範例顯示測量銷售量的 KPI。  
  
```  
  
<Property Name="InternetCurrSalesPerf" Type="Double">  
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
 [Csdl 的 BI 註解的技術參考](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
