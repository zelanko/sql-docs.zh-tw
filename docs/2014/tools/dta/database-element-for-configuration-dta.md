---
title: Database 元素 (DTA) 的組態 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fbca62a5d32ed6b7ec30eb5d6dba6a82a2b80c64
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747280"
---
# <a name="database-element-for-configuration-dta"></a>組態的 Database 元素 (DTA)
  指定 Database Engine Tuning Advisor 評估假設性組態 (`Configuration` 元素所指定) 時所針對的資料庫。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個 `Server` 元素需要這個元素一或多次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[組態的 Server 元素 &#40;DTA&#41;](server-element-for-configuration-dta.md)|  
|**子元素**|[資料庫的 Name 元素 &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [資料庫的 Schema 元素 &#40;DTA&#41;](schema-element-for-database-dta.md)<br /><br /> [Recommendation 元素 &#40;DTA&#41;](recommendation-element-dta.md)|  
  
## <a name="remarks"></a>備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **DatabaseTypecomplexType** 。 請勿混淆這個 `Database` 元素與根父系是在 XML 輸入檔頂端之 `Server` 元素的元素。 如需詳細資訊，請參閱[伺服器的 Database 元素 &#40;DTA&#41;](database-element-for-server-dta.md)。  
  
## <a name="example"></a>範例  
 如需使用方式的範例這`Database`項目，請參閱 <<c2> [ 含使用者指定組態的 XML 輸入檔範例&#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)。</c2>  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
