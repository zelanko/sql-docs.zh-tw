---
title: "Recommendation 元素 (DTA) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2d3402eb2554aa2342335b2901206dac1fbcf7a5
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

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
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 每個 **Table** 元素可以使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Table 元素的結構描述 &#40; Dta& &#41;](../../tools/dta/table-element-for-schema-dta.md)|  
|**子元素**|[Create 元素 &#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> **Drop** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。|  
  
## <a name="remarks"></a>備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **RecommendationTypecomplexType** 。 它用來指定假設性組態的索引。 請勿混淆這個 **Recommendation** 元素與可用來指定資料分割 (**RecommendationPType**) 或檢視 (**RecommendationViewType**) 的其他類型。 如需其他 **Recommendation** 元素類型的相關資訊，請參閱 [Database Engine Tuning Advisor XML Schema](http://go.microsoft.com/fwlink/?linkid=43100)(Database Engine Tuning Advisor XML 結構描述)。  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
