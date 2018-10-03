---
title: DimensionAttribute 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DimensionAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DimensionAttribute
helpviewer_keywords:
- DimensionAttribute data type
ms.assetid: 94349a87-b284-49d1-ac72-888f0375ceb8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4624e963a9bca0d7850d2936291d3a7515cac25f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106848"
---
# <a name="dimensionattribute-data-type-assl"></a>DimensionAttribute 資料類型 (ASSL)
  定義代表維度中某個屬性的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <Type>...</Type>  
   <Usage>...</Usage>  
   <Source>...</Source>  
   <EstimatedCount>...</EstimatedCount>  
   <KeyColumns>...</KeyColumns>  
   <NameColumn>...</NameColumn>  
   <ValueColumn>...</ValueColumn>  
   <Translations>...</Translations>  
   <AttributeRelationships>...</AttributeRelationships>  
   <DiscretizationMethod>...</DiscretizationMethod>  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   <RootMemberIf>...</RootMemberIf>  
   <OrderBy>...</OrderBy>  
   <DefaultMember>...</DefaultMember>  
   <OrderByAttributeID>...</OrderByAttributeID>  
   <SkippedLevelsColumn>...</SkippedLevelsColumn>  
   <NamingTemplate>...</NamingTemplate>  
   <MembersWithData>...</MembersWithData>  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
   <NamingTemplateTranslations>...</NamingTemplateTranslations>  
   <CustomRollupColumn>...</CustomRollupColumn>  
   <CustomRollupPropertiesColumn>...</CustomRollupPropertiesColumn>  
   <UnaryOperatorColumn>...</UnaryOperatorColumn>  
   <AttributeHierarchyOrdered>...</AttributeHierarchyOrdered>  
   <MemberNamesUnique>...</MemberNamesUnique>  
   <IsAggregatable>...</IsAggregatable>  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
   <AttributeHierarchyOptimizedState>...</AttributeHierarchyOptimizedState>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   <AttributeHierarchyDisplayFolder>...</AttributeHierarchyDisplayFolder>  
   <KeyUniquenessGuarantee>...<KeyUniquenessGuarantee>  
   <InstanceSelection>...</InstanceSelection>  
   <Annotations>...</Annotations>  
</DimensionAttribute>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|None|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[註釋](../collections/annotations-element-assl.md)， [AttributeHierarchyDisplayFolder](../properties/displayfolder-element-assl.md)， [AttributeHierarchyEnabled](../properties/enabled-element-assl.md)， [AttributeHierarchyOptimizedState](../properties/state-element-assl.md)， [AttributeHierarchyOrdered](../properties/attributehierarchyordered-element-assl.md)， [AttributeHierarchyVisible](../properties/visible-element-assl.md)， [AttributeRelationships](../collections/relationships-element-assl.md)， [CustomRollupColumn](../objects/column-element-assl.md)， [CustomRollupPropertiesColumn](../objects/customrolluppropertiescolumn-element-assl.md)， [DefaultMember](../objects/member-element-assl.md)，[描述](../properties/description-element-assl.md)， [DiscretizationBucketCount](../properties/discretizationbucketcount-element-assl.md)， [DiscretizationMethod](../properties/discretizationmethod-element-assl.md)， [EstimatedCount](../properties/estimatedcount-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [InstanceSelection](../properties/instanceselection-element-assl.md)， [IsAggregatable](../properties/isaggregatable-element-assl.md)，[KeyColumns](../collections/columns-element-assl.md)， [KeyUniquenessGuarantee](../properties/keyuniquenessguarantee-element-assl.md)， [MemberNamesUnique](../properties/membernamesunique-element-assl.md)， [MembersWithData](../objects/data-element-assl.md)， [MembersWithDataCaption](../properties/caption-element-assl.md)，[名稱](../properties/name-element-assl.md)， [NameColumn](../objects/namecolumn-element-assl.md)， [NamingTemplate](../properties/namingtemplate-element-assl.md)， [NamingTemplateTranslations](../collections/translations-element-assl.md)， [OrderBy](../properties/orderby-element-assl.md)， [OrderByAttributeID](../properties/attributeid-element-assl.md)， [RootMemberIf](../properties/rootmemberif-element-assl.md)， [SkippedLevelsColumn](../objects/skippedlevelscolumn-element-assl.md)，[來源](../properties/source-element-binding-assl.md)，[翻譯](../collections/translations-element-assl.md)，[型別](../properties/type-element-dimensionattribute-assl.md)， [UnaryOperatorColumn](../objects/unaryoperatorcolumn-element-assl.md)，[使用量](../properties/usage-element-dimensionattribute-assl.md)， [ValueColumn](../objects/valuecolumn-element-assl.md)|  
|衍生的元素|[屬性](../objects/attribute-element-assl.md)([屬性](../collections/attributes-element-assl.md)的集合[維度](../objects/dimension-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 在 DeploymentMode 組態屬性值 1 和 2 (SharePoint 和表格式模式，用來執行 PowerPivot 和表格式模型資料庫) 中執行服務時，適用下列限制：  
  
-   Usage 元素只接受 KEY 或 REGULAR 值。  
  
-   IsAggregatable 元素不得為 false。  
  
-   OrderBy 元素只接受 KEY 或 PROPERTYKEY 值。  
  
-   導出資料行在資料表中不得為主索引鍵。  
  
-   導出資料行在繫結中不得包含 DataSize。  
  
-   針對每個導出資料行，要在儲存屬性定義前執行語法驗證。  
  
-   若是 AttributeRelationships，RelationshipType 必須設為 Flexible 值。  
  
-   由 ‘RowNumber’ 識別的 ‘RowNumber’ 屬性必須擁有整數類型。  
  
-   只有 ‘RowNumber’ 屬性可以擁有 RowNumberBinding 類型的 KeyBinding。  
  
-   ‘RowNumber’ 之外的所有屬性都必須擁有 1 相對於索引鍵的基數 (除非屬性本身就是索引鍵)。  
  
-   當 OrderBy 指定的資料行也是 PropertyKey 時，OrderByAttributeId 無法指向資料列號碼資料行。  
  
-   當做索引鍵使用的屬性應該與其他所有屬性相關；不支援其他類型的關聯性。  
  
-   NullProcessing 元素無法設為 ‘UnknownMember’。  
  
-   Bindings 不得設為 ‘Value’。  
  
 在 DeploymentMode 組態屬性值 1 和 2 (SharePoint 和表格式模式，用來執行 PowerPivot 和表格式模型資料庫) 中執行服務時，不支援下列元素：  
  
-   AttributeHierarchyOptimizedState  
  
-   CustomRollupColumn  
  
-   CustomRollupPropertiesColumn  
  
-   DefaultMember  
  
-   DiscretizationBucketCount  
  
-   DiscretizationMethod  
  
-   SkippedLevelsColumn  
  
-   來源  
  
-   UnaryOperatorColumn  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
