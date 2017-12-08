---
title: "Language 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Language Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Language
- microsoft.xml.analysis.language
- http://schemas.microsoft.com/analysisservices/2003/engine#Language
helpviewer_keywords: Language element
ms.assetid: cd998202-e43f-4c6c-8727-a15a76a520ea
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a378b193d0665672ad9d423e10bec65dac23810a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="language-element-xmla"></a>Language 元素 (XMLA)
  包含父代的地區設定識別碼 (LCID)[轉譯](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Translation>  
   ...  
   <Language>...</Language>  
   ...  
</Translation>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[轉譯](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **語言**項目會指定父系所使用的 LCID**轉譯**指派的項目**名稱**父元素之**轉譯**屬性成員，針對指定的語言項目期間**插入**或**更新**命令。  
  
## <a name="see-also"></a>請參閱＜  
 [插入項目 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Name 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md)   
 [Update 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
