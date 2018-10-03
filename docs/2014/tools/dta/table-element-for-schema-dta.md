---
title: 資料表項目結構描述 (DTA) |Microsoft Docs
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
- Table element [DTA]
ms.assetid: a59e8319-05d1-47f3-af39-7d970ab8e7dc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c7d85b45ff292d4262393542909566b233de882d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074412"
---
# <a name="table-element-for-schema-dta"></a>結構描述的 Table 元素 (DTA)
  指定要微調的資料表。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Schema>  
...code removed here...  
    <Table>...</Table>  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|`NumberOfRows`|選擇性。 可讓您模擬不同大小的資料表之整數。|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|**string**，在 1 和 255 個字元之間。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 依照工作負載的需要，列出儘可能多的資料表。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[資料庫的 schema 元素&#40;DTA&#41;](schema-element-for-database-dta.md)|  
|**子元素**|[資料表名稱項目&#40;DTA&#41;](name-element-for-table-dta.md)|  
  
## <a name="remarks"></a>備註  
 如果您沒有指定 `Table` 元素，Database Engine Tuning Advisor 會假設指定資料庫的所有資料表都可以微調。  
  
## <a name="example"></a>範例  
 如需使用範例，請參閱[伺服器元素 &#40;DTA&#41;](server-element-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
