---
title: Database 元素 (DTA) 伺服器 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 34bd7e9b2437adedd9a65032d16a6093ea01f634
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032451"
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
|出現次數|需要一或多次，每個`Server`項目。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|父元素|[Server 元素&#40;DTA&#41;](server-element-dta.md)|  
|子元素|[資料庫名稱元素&#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [資料庫的 schema 元素&#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **DatabaseDetailsTypecomplexType** 。 請勿混淆這個 `Database` 元素與根父系是 `Configuration` 元素的元素。 如需詳細資訊，請參閱[組態的 Database 元素 &#40;DTA&#41;](database-element-for-configuration-dta.md)。  
  
## <a name="example"></a>範例  
 如需使用範例的`Database`項目，請參閱[伺服器項目&#40;DTA&#41;](server-element-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  