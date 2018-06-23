---
title: 資料行索引的元素 (DTA) |Microsoft 文件
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
- Column element
ms.assetid: ba9fac20-26bd-4333-940e-842c15241b46
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 58d8827fe160ef1acb300e7501fd9faeaa369efd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023237"
---
# <a name="column-element-for-index-dta"></a>索引的 Column 元素 (DTA)
  指定針對使用者指定的組態來建立索引的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Create>  
  <Index>  
    <Name>...</Name>  
    <Column [Type | SortOrder]>  
     ...code removed here...  
     </Column>  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|資料行屬性|描述|  
|----------------------|-----------------|  
|`Type`|選擇性。 指定索引資料行類型。 請利用 **string** 資料類型和下列其中一個允許的值，來指定這個屬性：<br /><br /> `KeyColumn`：<br />                  指定由索引鍵參考資料行。 請利用下列語法來設定這個屬性：<br />`<Column Type="KeyColumn">`<br />如需索引鍵資料行的詳細資訊，請參閱 [叢集與非叢集索引說明](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)。<br /><br /> `IncludedColumn`： 指定資料行是一個內含資料行 （而不是索引鍵的資料行）。 請利用下列語法來設定這個屬性：<br />`<Column Type="IncludedColumn">`<br />如需內含資料行的詳細資訊，請參閱 [建立內含資料行的索引](../../relational-databases/indexes/create-indexes-with-included-columns.md)。|  
|`SortOrder`|選擇性。 指定資料行的排序順序。 請依照下列方式，利用 **string** 資料類型來指定「遞增」或「遞減」排列順序：<br /><br /> `<Column SortOrder="Ascending">`|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|`Index` 元素可以指定最多 1024 個資料行。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[索引項目&#40;DTA&#41;](index-element-dta.md)|  
|**子元素**|[資料行名稱元素&#40;DTA&#41;](name-element-for-column-dta.md)|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  