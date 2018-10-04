---
title: EntityType 元素 (CSDLBI) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 372e2c13-ec38-4bb1-981c-50758d59a1da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f3d1db1998e91eedf4ebc8f759550b2088a29d03
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48139988"
---
# <a name="entitytype-element-csdlbi"></a>EntityType 元素 (CSDLBI)
  `EntityType` 元素是複雜類型，代表資料模型中高層級實體的結構，例如客戶或訂單。 `bi:EntityType`項目延伸的定義[EntityType](http://msdn.microsoft.com/library/bb399206.aspx)用於[實體資料架構](/dotnet/framework/data/adonet/ef/overview)。  
  
 系統必須針對資料模型中包含的每個實體指定 EntityType 元素。 EntityType 的子元素會描述資料表中的資料行和量值。 資料表之間的關聯性包含在 `EntityContainer` 中。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出元素和定義 `EntityType` 元素的屬性。 另請參閱適用於屬性[EntityType](http://msdn.microsoft.com/library/bb399206.aspx)項目。  
  
|名稱|是否必要|描述|  
|----------|-----------------|-----------------|  
|目錄|否|字串，其中包含資料行中可能的資料類型。 此值衍生自資料模型中 DimensionAttributeTypeEnumType 的值。<br /><br /> 如果 DimensionAttributeTypeEnumType 的值為 "ExtendedType"，則 Contents 的值會衍生自 DimensionAttribute 的 ExtendedType 元素。 用戶端不需要回應這些值。|  
|DefaultDetails|否|屬性參考的清單，代表資料表中的資料行集。<br /><br /> 請參閱[DefaultDetails 元素&#40;CSDLBI&#41;](defaultdetails-element-csdlbi.md)。|  
|DefaultImage|否|包含說明實體之影像的資料行參考。<br /><br /> 在多維度模型中，此元素對應維度屬性上的二進位屬性。 如果此屬性存在，則元素必須只包含單獨一個 MemberRef 元素。<br /><br /> 請參閱[MemberRef 元素&#40;CSDLBI&#41;](memberref-element-csdlbi.md)。|  
|DefaultMeasure|否|實體中量值的參考，應在對實體進行計算時用做預設值。 如果未指定，則預設值為 SUM。<br /><br /> 請參閱[MemberRef 元素&#40;CSDLBI&#41;](memberref-element-csdlbi.md)。|  
|DisplayKey|否|資料行或角色端的參考清單，此清單構成可唯一識別實體執行個體的強式識別碼。<br /><br /> 請參閱[DisplayKey 元素&#40;CSDLBI&#41;](displaykey-element-csdlbi.md)。|  
|階層|否|模型中階層的清單。<br /><br /> 請參閱[Hierarchy 元素&#40;CSDLBI&#41;](hierarchy-element-csdlbi.md)。|  
|ReferenceName|是|可用於在 Data Analysis Expressions (DAX) 查詢中參考此實體的識別碼。<br /><br /> 如果此屬性不存在，則會使用實體的完整欄位名稱。|  
|SortMembers|否|要排序的屬性清單。 SortDirection 屬性會指出次序為遞增或遞減。|  
  
## <a name="contents-element"></a>Contents 元素  
 `Contents` 元素是簡單類型，用於描述實體中資料的類型。  
  
 實體 (資料行) 的內容可以是下列任何值：  
  
|值|描述|  
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
|CURRENCY|包含貨幣資料和中繼資料。|  
|匯率|代表貨幣匯率資訊的屬性。|  
|通道|代表通路資訊的屬性。|  
|促銷|代表行銷促銷資訊的屬性。|  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列範例顯示 AdventureWorks 表格式模型中所使用 CSDLBI 1.1 版 Geography 資料表的一部分。 RowNumber 資料行為隱藏資料行，會自動產生做為表格式模型中的資料列識別碼，因此擁有 Contents 屬性 `RowNumber`。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [CSDL 之 BI 註解的技術參考](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
