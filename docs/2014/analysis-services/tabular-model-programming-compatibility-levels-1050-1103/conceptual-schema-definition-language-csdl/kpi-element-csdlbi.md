---
title: KPI 元素 (CSDLBI) |Microsoft Docs
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
ms.assetid: 203ee6e8-eef2-4476-b09f-bd95e492ddaa
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a649ffffe6f2d9f5902ede9e6d7a6126fd09e25
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37155079"
---
# <a name="kpi-element-csdlbi"></a>KPI 元素 (CSDLBI)
  Kpi 元素會定義可當做關鍵效能指標 (KPI) 使用的計算。 在商業智慧資料模型中，KPI 是以量值為基礎，因此 KPI 的定義會包含與量值關聯的所有中繼資料以及呈現 KPI 值所需的資訊，包括預設圖形。  
  
 Kpi 元素不會指定包含在量值定義中的公式，而是指定與當做 KPI 使用之量值相關聯的其他中繼資料。 一旦您將量值指定為 KPI 之後，就無法將它當做量值用於其他內容。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 Kpi 元素的元素和屬性。  
  
|名稱|是否必要|描述|  
|----------|-----------------|-----------------|  
|文件集|否|KPI 的描述。|  
|KpiGoal|是|資料行的參考，其中包含可用來做為目標的值。<br /><br /> 請參閱 [PropertyRef 元素 &#40;CSDLBI&#41;](propertyref-element-csdlbi.md)。|  
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
 [CSDL 之 BI 註解的技術參考](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
