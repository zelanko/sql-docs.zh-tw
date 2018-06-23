---
title: Hierarchy 資料類型 (ASSL) |Microsoft 文件
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
api_name:
- Hierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Hierarchy data type
ms.assetid: 2e05917e-7e5d-4dd1-817b-4ff5647747ff
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 14354458e3441c6f8f2691350e9236f2aecb6cdd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146192"
---
# <a name="hierarchy-data-type-assl"></a>Hierarchy 資料類型 (ASSL)
  定義代表維度中某個階層的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Hierarchy>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <DisplayFolder>...</DisplayFolder>  
   <Translations>...</Translations>  
   <AllMemberName>...</AllMemberName>  
   <AllMemberTranslations>...</AllMemberTranslation>  
   <MemberNamesUnique>...</MemberNamesUnique>  
   <AllowDuplicateNames>...</AllowDuplicateNames>  
   <Levels>...</Levels>  
   <Annotations>...</Annotation>  
</Hierarchy>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[AllMemberName](../properties/name-element-assl.md)、 [AllMemberTranslations](../collections/translations-element-assl.md)、 [AllowDuplicateNames](../properties/allowduplicatenames-element-assl.md)、 [Annotations](../collections/annotations-element-assl.md)、 [Description](../properties/description-element-assl.md)、 [DisplayFolder](../properties/displayfolder-element-assl.md)、 [ID](../properties/id-element-assl.md)、 [Levels](../collections/levels-element-assl.md)、 [MemberNamesUnique](../properties/membernamesunique-element-assl.md)、 [Name](../properties/name-element-assl.md)、 [Translations](../collections/translations-element-assl.md)|  
|衍生的元素|[Hierarchy](../objects/hierarchy-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 SharePoint 或表格式伺服器模式的 DevelopmentMode 1 或 2 下各不支援 *MemberNamesUnique* 元素。  
  
 SharePoint 或表格式伺服器模式的 DevelopmentMode 1 或 2 下各不支援 *MemberKeysUnique* 元素。  
  
 SharePoint 或表格式伺服器模式的 DevelopmentMode 1 或 2 下各不支援 *AllowDuplicateNames* 元素。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Hierarchy>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  