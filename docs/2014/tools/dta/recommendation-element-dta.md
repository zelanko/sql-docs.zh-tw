---
title: Recommendation 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6bd7c8b2315f853166e4172030aa191748506b27
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37260059"
---
# <a name="recommendation-element-dta"></a>Recommendation 元素 (DTA)
  包含屬於使用者指定組態之一部份的假設性索引的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Configuration>  
    ...code removed here...  
    <Table>  
      <Name>...</Name>  
      <Recommendation>  
      ...code removed here...  
      </Recommendation>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 可以為每一次使用`Table`項目。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[資料表結構描述的項目&#40;DTA&#41;](table-element-for-schema-dta.md)|  
|**子元素**|[建立項目&#40;DTA&#41;](create-element-dta.md)<br /><br /> `Drop` 項目。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。|  
  
## <a name="remarks"></a>備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **RecommendationTypecomplexType** 。 它用來指定假設性組態的索引。 請勿混淆這個`Recommendation`可用來指定資料分割的其他類型的項目 (`RecommendationPType`) 或檢視表 (`RecommendationViewType`)。 如需其他資訊`Recommendation`項目類型，請參閱[Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)。  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
