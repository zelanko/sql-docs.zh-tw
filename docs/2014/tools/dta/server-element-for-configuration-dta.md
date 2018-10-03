---
title: 伺服器組態的元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10a8fa9eed7f89d9706ab3388eccc881b165ef74
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206908"
---
# <a name="server-element-for-configuration-dta"></a>組態的 Server 元素 (DTA)
  包含 Database Engine Tuning Advisor 評估假設性組態伺服器的識別資訊 (所指定`Configuration`項目)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每一次需要`Configuration`項目。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[組態項目&#40;DTA&#41;](configuration-element-dta.md)|  
|**子元素**|[伺服器名稱項目&#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [組態的 database 元素&#40;DTA&#41;](database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>備註  
 您可以指定只有一個`Server`項目`Configuration`項目。 在 **Database Engine Tuning Advisor XML 結構描述** 中，這個元素的名稱為 [ServerTypecomplexType](http://go.microsoft.com/fwlink/?linkid=43100)。 請勿混淆這個`Server`元素和子系的`DTAInput`項目。 如需詳細資訊，請參閱 [Server 元素 &#40;DTA&#41;](server-element-dta.md)。  
  
## <a name="example"></a>範例  
 如需使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
