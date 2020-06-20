---
title: Configuration （DTA）的 Server 元素 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1d569373f80a2f5488e8612cc30da264d283cd7f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85007650"
---
# <a name="server-element-for-configuration-dta"></a>組態的 Server 元素 (DTA)
  包含 Database Engine Tuning Advisor 評估假設性組態 (`Configuration` 元素所指定) 時所在之伺服器的識別資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|(必要) 每個 `Configuration` 元素出現一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Configuration 元素 &#40;DTA&#41;](configuration-element-dta.md)|  
|**子元素**|[伺服器的 Name 元素 &#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [組態的 Database 元素 &#40;DTA&#41;](database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>備註  
 您只能 `Server` 為元素指定一個元素 `Configuration` 。 在 **Database Engine Tuning Advisor XML 結構描述** 中，這個元素的名稱為 [ServerTypecomplexType](https://go.microsoft.com/fwlink/?linkid=43100)。 請勿混淆這個 `Server` 元素和 `DTAInput` 元素的子元素。 如需詳細資訊，請參閱 [Server 元素 &#40;DTA&#41;](server-element-dta.md)。  
  
## <a name="example"></a>範例  
 如需使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
