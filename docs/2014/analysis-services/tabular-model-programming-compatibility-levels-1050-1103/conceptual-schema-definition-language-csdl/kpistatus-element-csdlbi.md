---
title: KpiStatus 元素 (CSDLBI) |Microsoft Docs
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
ms.assetid: 6fee5b82-caa8-46a1-ad68-bbce3e11e01e
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a72905e91bb27ffb8acff7fb391e38d59e14209
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271664"
---
# <a name="kpistatus-element-csdlbi"></a>KpiStatus 元素 (CSDLBI)
  KpiStatus 元素會定義包含在關鍵效能指標 (KPI) 中當做狀態指標使用之值的資料行參考。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 KpiStatus 元素的元素和屬性。  
  
|名稱|是否必要|描述|  
|----------|-----------------|-----------------|  
|PropertyRef|是|包含在 KPI 中當做狀態指標使用之值的資料行參考。<br /><br /> 此元素「必須」只包含單獨一個資料行參考，如 TPropertyRefcomplex 類型所定義。|  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 CSDLBI 1.1 版中的範例顯示 AdventureWorks 表格式模型範例中的 KPI。 KpiStatus 元素會參考包含值的資料行 (表示為 PropertyRef)。  
  
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
  
 下列 CSDLBI 1.1 版中的範例會顯示來自 Contoso Operations Cube 的 KPI。 KpiStatus 元素會參考計算 KPI 狀態值的量值。  
  
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
 [KPI 元素&#40;CSDLBI&#41;](kpi-element-csdlbi.md)  
  
  
