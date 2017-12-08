---
title: "EntityType 元素 (CSDLBI) |Microsoft 文件"
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
ms.assetid: 372e2c13-ec38-4bb1-981c-50758d59a1da
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f5b62cad891d4d02120b3325d57e327e299ef1be
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="entitytype-element-csdlbi"></a>EntityType 元素 (CSDLBI)
  **EntityType**元素是複雜類型表示的高層級的實體，例如客戶或訂單，資料模型中的結構。 **Bi: EntityType**項目延伸的定義[EntityType](http://msdn.microsoft.com/library/bb399206.aspx)用於[實體資料架構](http://msdn.microsoft.com/library/bb399567.aspx)。  
  
 系統必須針對資料模型中包含的每個實體指定 EntityType 元素。 EntityType 的子元素會描述資料表中的資料行和量值。 資料表之間的關聯性都會納入**EntityContainer**。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出的項目和屬性，定義**EntityType**項目。 另請參閱適用於屬性[EntityType](http://msdn.microsoft.com/library/bb399206.aspx)項目。  
  
|名稱|是否必要|Description|  
|----------|-----------------|-----------------|  
|目錄|否|字串，其中包含資料行中可能的資料類型。 此值衍生自資料模型中 DimensionAttributeTypeEnumType 的值。<br /><br /> 如果 DimensionAttributeTypeEnumType 的值為 "ExtendedType"，則 Contents 的值會衍生自 DimensionAttribute 的 ExtendedType 元素。 用戶端不需要回應這些值。|  
|DefaultDetails|否|屬性參考的清單，代表資料表中的資料行集。<br /><br /> 請參閱[DefaultDetails 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/defaultdetails-element-csdlbi.md).|  
|DefaultImage|否|包含說明實體之影像的資料行參考。<br /><br /> 在多維度模型中，此元素對應維度屬性上的二進位屬性。 如果此屬性存在，則元素必須只包含單獨一個 MemberRef 元素。<br /><br /> 請參閱[MemberRef 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md).|  
|DefaultMeasure|否|實體中量值的參考，應在對實體進行計算時用做預設值。 如果未指定，則預設值為 SUM。<br /><br /> 請參閱[MemberRef 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md).|  
|DisplayKey|否|資料行或角色端的參考清單，此清單構成可唯一識別實體執行個體的強式識別碼。<br /><br /> 請參閱[DisplayKey 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/displaykey-element-csdlbi.md).|  
|階層|否|模型中階層的清單。<br /><br /> 請參閱[Hierarchy 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/hierarchy-element-csdlbi.md).|  
|ReferenceName|是|可用於在 Data Analysis Expressions (DAX) 查詢中參考此實體的識別碼。<br /><br /> 如果此屬性不存在，則會使用實體的完整欄位名稱。|  
|SortMembers|否|要排序的屬性清單。 SortDirection 屬性會指出次序為遞增或遞減。|  
  
## <a name="contents-element"></a>Contents 元素  
 **內容**元素是簡單類型，描述實體中的資料類型。  
  
 實體 (資料行) 的內容可以是下列任何值：  
  
|值|說明|  
|-----------|-----------------|  
|一般|未另行定義。|  
|Time|代表時間週期的屬性，例如年數、半年數、季數、月數或日數。|  
|Geography|代表地理資訊的屬性，例如城市或郵遞區號。|  
|組織|代表組織資訊的屬性，例如員工或分公司。|  
|BillOfMaterials|代表存貨或製造資訊的屬性，例如產品的組件清單。|  
|帳戶|屬性代表財務報表的帳戶圖表。|  
|客戶|代表客戶或連絡資訊的屬性。|  
|產品|代表產品資訊的屬性。|  
|狀況|代表計畫或策略分析資訊的屬性。|  
|數量的|代表數量資訊的屬性。|  
|公用程式|代表其他資訊的屬性。|  
|貨幣|包含貨幣資料和中繼資料。|  
|匯率|代表貨幣匯率資訊的屬性。|  
|通道|代表通路資訊的屬性。|  
|促銷|代表行銷促銷資訊的屬性。|  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列範例顯示 AdventureWorks 表格式模型中所使用 CSDLBI 1.1 版 Geography 資料表的一部分。 RowNumber 資料行是隱藏的資料行自動產生做為表格式模型中的資料列識別碼，因此擁有 Contents 屬性**RowNumber**。  
  
```  
  
<EntityType   
     Name="DimGeography">  
     <Key>  
        <PropertyRef Name="RowNumber" />  
     </Key>  
     <Property   
        Name="RowNumber"   
        Type="Int64" Nullable="false">  
     <bi:Property   
        Hidden="true"   
        Contents="RowNumber"   
        Stability="RowNumber" />  
     </Property>  
....  
  
```  
  
## <a name="example"></a>範例  
 **多維度**  
  
 下列範例顯示 CSDLBI 1.1 版中的 EntityType 元素，代表 Contoso Operations Cube 中時間維度的一部分。  
  
```  
<EntityType   
       Name="CalendarQuarter">  
    <Key>  
       <PropertyRef Name="RowNumber" />  
    </Key>  
  
    <Property Name="RowNumber"   
       Type="Int64"   
       Nullable="false">  
    <bi:Property   
       Hidden="true"   
       Contents="RowNumber"   
       Stability="RowNumber"   
    />  
    </Property>  
  
    <Property Name="CalendarQuarter2"   
       Type="String"   
       MaxLength="Max"   
       Unicode="true"   
       FixedLength="false"   
       Nullable="false">  
    <bi:Property   
       Caption="CalendarQuarter"   
       ReferenceName="CalendarQuarter"   
    />  
    </Property>  
   <bi:EntityType />  
</EntityType>  
```  
  
## <a name="see-also"></a>請參閱＜  
 [CSDL 之 BI 註解的技術參考](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
