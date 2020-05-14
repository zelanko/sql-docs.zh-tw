---
title: 索引的 Column 元素 (DTA)
description: 在 DTA 公用程式中，索引其 Column 元素會針對使用者所指定組態來指定要建立索引的資料行。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Column element
ms.assetid: ba9fac20-26bd-4333-940e-842c15241b46
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/09/2017
ms.openlocfilehash: 02900685d93eef62553d830494d25ec83ca83ce1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831624"
---
# <a name="column-element-for-index-dta"></a>索引的 Column 元素 (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
  
 **類型**：選擇性。 指定索引資料行類型。 請利用 **string** 資料類型和下列其中一個允許的值，來指定這個屬性：  
  
-   **KeyColumn**  
  
     指定由索引鍵參考資料行。 請利用下列語法來設定這個屬性：  
  
    ```  
    <Column Type="KeyColumn">  
    ```  
  
     如需索引鍵資料行的詳細資訊，請參閱 [叢集與非叢集索引說明](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)。  
  
-   **IncludedColumn**  
  
     指定資料行是一個內含資料行 (而不是索引鍵資料行)。 請利用下列語法來設定這個屬性：  
  
    ```  
    <Column Type="IncludedColumn">  
    ```  
  
     如需內含資料行的詳細資訊，請參閱 [建立內含資料行的索引](../../relational-databases/indexes/create-indexes-with-included-columns.md)。  
  
 **SortOrder**：選擇性。 指定資料行的排序順序。 請依照下列方式，利用 **string** 資料類型來指定「遞增」  或「遞減」  排列順序：  
  
```  
<Column SortOrder="Ascending">  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|**Index** 元素可以指定最多 1024 個資料行。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Index 元素 &#40;DTA&#41;](../../tools/dta/index-element-dta.md)|  
|**子元素**|[資料行的 Name 元素 &#40;DTA&#41;](../../tools/dta/name-element-for-column-dta.md)|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
