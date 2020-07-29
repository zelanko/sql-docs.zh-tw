---
title: OnlineIndexOperation 元素 (DTA)
description: 在 dta 公用程式中，OnlineIndexOperation 元素會指定是否可以在線上建立 Database Engine Tuning Advisor 建議的項目。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- OnlineIndexOperation element
ms.assetid: 7c5614cd-09aa-4a59-9591-347aa7d36473
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: b9299786ce9c71c393c1c0b270b345092296d7ac
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775002"
---
# <a name="onlineindexoperation-element-dta"></a>OnlineIndexOperation 元素 (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

指定是否能夠在線上建立 Database Engine Tuning Advisor 建議的索引、索引檢視或資料分割。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <OnlineIndexOperation>...</OnlineIndexOperation>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|**字串**，沒有最大長度。|  
|**允許的值**|**OFF**<br /> 不能在線上建立任何建議的實體設計結構。<br /><br /> **ON**<br /> 可以在線上建立所有建議的實體設計結構。<br /><br /> **MIXED**<br /> Database Engine Tuning Advisor 嘗試建議在可能的情況下，能夠在線上建立的實體設計結構。<br /><br /> 這個元素使用這些值的其中之一。 如果在線上建立索引，就會在它的物件定義上附加關鍵字 **ONLINE = ON** 。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 如果使用這個元素的話， **TuningOptions** 元素只能使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[簡單 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
