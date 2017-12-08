---
title: "DimensionAttribute 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DimensionAttribute Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DimensionAttribute
helpviewer_keywords: DimensionAttribute data type
ms.assetid: 94349a87-b284-49d1-ac72-888f0375ceb8
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4070c34393b5704950431921646607d5c86f33fb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
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
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [AttributeHierarchyDisplayFolder](../../../analysis-services/scripting/properties/attributehierarchydisplayfolder-element-assl.md)， [AttributeHierarchyEnabled](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)， [AttributeHierarchyOptimizedState](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md)， [AttributeHierarchyOrdered](../../../analysis-services/scripting/properties/attributehierarchyordered-element-assl.md)， [AttributeHierarchyVisible](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md)， [AttributeRelationships](../../../analysis-services/scripting/collections/attributerelationships-element-assl.md)， [CustomRollupColumn](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)， [CustomRollupPropertiesColumn](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)， [DefaultMember](../../../analysis-services/scripting/properties/defaultmember-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)， [DiscretizationBucketCount](../../../analysis-services/scripting/properties/discretizationbucketcount-element-assl.md)， [DiscretizationMethod](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md)， [EstimatedCount](../../../analysis-services/scripting/properties/estimatedcount-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)，[InstanceSelection](../../../analysis-services/scripting/properties/instanceselection-element-assl.md)， [IsAggregatable](../../../analysis-services/scripting/properties/isaggregatable-element-assl.md)， [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)， [KeyUniquenessGuarantee](../../../analysis-services/scripting/properties/keyuniquenessguarantee-element-assl.md)， [MemberNamesUnique](../../../analysis-services/scripting/properties/membernamesunique-element-assl.md)， [MembersWithData](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)， [MembersWithDataCaption](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)， [NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)， [NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md)， [NamingTemplateTranslations](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md)， [OrderBy](../../../analysis-services/scripting/properties/orderby-element-assl.md)， [OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md)， [RootMemberIf](../../../analysis-services/scripting/properties/rootmemberif-element-assl.md)， [SkippedLevelsColumn](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)， [來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)，[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)，[類型](../../../analysis-services/scripting/properties/type-element-dimensionattribute-assl.md)， [UnaryOperatorColumn](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)，[使用量](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)， [ValueColumn](../../../analysis-services/scripting/objects/valuecolumn-element-assl.md)|  
|衍生的元素|[屬性](../../../analysis-services/scripting/objects/attribute-element-assl.md)([屬性](../../../analysis-services/scripting/collections/attributes-element-assl.md)集合[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 在 DeploymentMode 組態屬性值 1 和 2 中執行服務時，適用下列限制 (SharePoint 和表格式模式，用來執行[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]和表格式模型資料庫):  
  
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
  
 在 DeploymentMode 組態屬性值 1 和 2 執行服務時，不支援下列項目 (SharePoint 和表格式模式，用來執行[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]和表格式模型資料庫):  
  
-   AttributeHierarchyOptimizedState  
  
-   CustomRollupColumn  
  
-   CustomRollupPropertiesColumn  
  
-   DefaultMember  
  
-   DiscretizationBucketCount  
  
-   DiscretizationMethod  
  
-   SkippedLevelsColumn  
  
-   Source  
  
-   UnaryOperatorColumn  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
