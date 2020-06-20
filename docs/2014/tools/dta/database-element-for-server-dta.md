---
title: 伺服器的 Database 元素（DTA） |Microsoft Docs
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
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: stevestein
ms.author: sstein
ms.openlocfilehash: 87df538858c9294cb8986da3df0d2b3814411326
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85057754"
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無。|  
|預設值|無。|  
|出現次數|每個 `Server` 元素需要這個元素一或多次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|父元素|[Server 元素 &#40;DTA&#41;](server-element-dta.md)|  
|子元素|[資料庫的 Name 元素 &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [資料庫的 Schema 元素 &#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **DatabaseDetailsTypecomplexType** 。 請勿混淆這個 `Database` 元素與根父系是 `Configuration` 元素的元素。 如需詳細資訊，請參閱[組態的 Database 元素 &#40;DTA&#41;](database-element-for-configuration-dta.md)。  
  
## <a name="example"></a>範例  
 如需元素的使用範例 `Database` ，請參閱[Server 元素 &#40;DTA&#41;](server-element-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
