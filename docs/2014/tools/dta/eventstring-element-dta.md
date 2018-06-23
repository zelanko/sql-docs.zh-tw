---
title: EventString 元素 (DTA) |Microsoft 文件
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
- EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6155627f60694cf1a21d39893e40b106b9df0886
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030195"
---
# <a name="eventstring-element-dta"></a>EventString 元素 (DTA)
  在 XML 輸入檔中，直接指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼工作負載。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Workload>  
    <EventString Weight="...">  
    ...code removed here...  
    </EventString>  
</Workload>  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|`Weight`|選擇性。 針對指定事件來指定查詢加權因數 (重要性因數)。 使用`float`資料類型來指定加權。 例如，`Weight`="100.01"。 `Weight` 所能指定的最小值是 "0"。|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|`string`長度沒有限制。|  
|**預設值**|無。|  
|**出現次數**|如果未指定任何其他工作負載類型，便需要使用這個元素一次。 您必須指定`EventString`、 `File`，或`Database`子元素`Workload`父代，但只有一個型別使用。 例如，如果您指定的工作負載`EventString`元素，則您也不能指定的工作負載`File`相同 XML 輸入檔中的項目。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Workload 元素&#40;DTA&#41;](workload-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 此元素的使用方式範例，請參閱 [XML Input File Sample with Inline Workload &#40;DTA&#41;](xml-input-file-sample-with-inline-workload-dta.md) (內嵌工作負載的 XML 輸入檔範例 (DTA))。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  