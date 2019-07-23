---
title: EventString 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 157c50f419b7003a9dde862c3a2c74c4033fe794
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008797"
---
# <a name="eventstring-element-dta"></a>EventString 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
|attribute|Description|  
|---------------|-----------------|  
|**Weight**|選擇性。 針對指定事件來指定查詢加權因數 (重要性因數)。 請利用 **float** 資料類型來指定加權。 例如， **Weight**="100.01"。 **Weight** 所能指定的最小值是 "0"。|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|Description|  
|--------------------|-----------------|  
|**資料類型和長度**|**string**，沒有長度限制。|  
|**預設值**|無。|  
|**出現次數**|如果未指定任何其他工作負載類型，便需要使用這個元素一次。 您必須指定 **EventString**父系的 **File**、 **Database** 或 **Workload** 子元素，但只能使用一種類型。 例如，如果您利用 **EventString** 元素指定了工作負載，便不能在相同 XML 輸入檔中，同時利用 **File** 元素來指定工作負載。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Workload 元素 &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 此元素的使用方式範例，請參閱 [XML Input File Sample with Inline Workload &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md) (內嵌工作負載的 XML 輸入檔範例 (DTA))。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
