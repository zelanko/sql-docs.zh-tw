---
title: "Database 元素 (DTA) 伺服器 |Microsoft 文件"
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
- Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3b24e80cb9f0686e3f6eac488488d001e1076ae3
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="database-element-for-server-dta"></a>伺服器的 Database 元素 (DTA)
  指定特定伺服器中需要微調的資料庫。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無。|  
|預設值|無。|  
|出現次數|每個 **Server** 元素需要這個元素一或多次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|父元素|[Server 元素 &#40;DTA&#41;](../../tools/dta/server-element-dta.md)|  
|子元素|[資料庫的 Name 元素 &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [資料庫的 Schema 元素 &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **DatabaseDetailsTypecomplexType** 。 請勿混淆這個 **Database** 元素與根父系是 **Configuration** 元素的元素。 如需詳細資訊，請參閱[組態的 Database 元素 &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)。  
  
## <a name="example"></a>範例  
 如需 **Database** 元素的使用範例，請參閱 [Server 元素 &#40;DTA&#41;](../../tools/dta/server-element-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

