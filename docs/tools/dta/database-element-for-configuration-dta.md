---
title: "Database 元素 (DTA) 組態 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
caps.latest.revision: "12"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 02fc044ef6ce1e015743ee503ed77ea843b0e182
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="database-element-for-configuration-dta"></a>組態的 Database 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]指定要針對 Database Engine Tuning Advisor 評估假設性組態的資料庫 (所指定**組態**項目)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個 **Server** 元素需要這個元素一或多次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[伺服器項目組態 &#40; Dta& &#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
|**子元素**|[資料庫 &#40; Dta& &#41; 的 name 元素](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [結構描述項目資料庫 &#40; Dta& &#41;](../../tools/dta/schema-element-for-database-dta.md)<br /><br /> [Recommendation 元素 &#40; Dta& &#41;](../../tools/dta/recommendation-element-dta.md)|  
  
## <a name="remarks"></a>備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **DatabaseTypecomplexType** 。 請勿混淆這個 **Database** 元素與根父系是在 XML 輸入檔頂端之 **Server** 元素的元素。 如需詳細資訊，請參閱[伺服器的 Database 元素 &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)。  
  
## <a name="example"></a>範例  
 如需此 **Database** 元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
