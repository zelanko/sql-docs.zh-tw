---
title: Translation 元素 (XMLA) |Microsoft Docs
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
- Translation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Translation
- microsoft.xml.analysis.translation
- http://schemas.microsoft.com/analysisservices/2003/engine#Translation
helpviewer_keywords:
- Translation element
ms.assetid: ce962d4b-dda9-4a16-a56c-ff7a5275c48a
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ce94966eae0cb1088ff462f551bdd27ad4304ee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180785"
---
# <a name="translation-element-xmla"></a>Translation 元素 (XMLA)
  定義屬性成員的翻譯。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Translations>  
   ...  
   <Translation>  
      <Language>...</Language>  
      <Name>...</Name>  
   </Translation>  
   ...  
</Translations>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[翻譯](translations-element-xmla.md)|  
|子元素|[語言](language-element-xmla.md)，[名稱](name-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 A`Translation`項目會定義將屬性成員定義的期間指定的屬性轉譯為所需的資訊[插入](../xml-elements-commands/insert-element-xmla.md)或是[更新](../xml-elements-commands/update-element-xmla.md)命令。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
