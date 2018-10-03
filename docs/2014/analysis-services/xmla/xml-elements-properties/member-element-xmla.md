---
title: Member 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Member Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Member
- microsoft.xml.analysis.member
- http://schemas.microsoft.com/analysisservices/2003/engine#Member
helpviewer_keywords:
- Member element
ms.assetid: 5cc33a1f-192e-4821-a4ef-9a5f2bb7a9f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8ab24b02a46a5e6416018d9f77c733b0d3de7153
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168968"
---
# <a name="member-element-xmla"></a>Member 元素 (XMLA)
  表示父代中的單一成員[成員](members-element-xmla.md)或是[Tuple](tuple-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Members>  
   ...  
   <Member>  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Members>  
<!-- or -->  
<Tuple>  
   ...  
   <Member Hierarchy="string">  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Tuple>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[成員](members-element-xmla.md)， [Tuple](tuple-element-xmla.md)|  
|子元素|[Caption](caption-element-xmla.md)， [DisplayInfo](displayinfo-element-xmla.md)， [LName](name-element-xmla.md)， [LNum](lnum-element-xmla.md)， [UName](uname-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|階層|必要的 `String` 屬性 (僅適用於 `Tuple` 父元素)。 `Member` 元素所代表之成員所屬的階層名稱。|  
  
## <a name="remarks"></a>備註  
 `Member` 元素包含在給定階層內部識別和顯示成員所需的資訊。 若為 `Members` 父元素，表示階層已經由父元素的 `Hierarchy` 屬性指定。 若為 `Tuple` 父元素，表示階層是使用 `Hierarchy` 元素的 `Member` 屬性指定的。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
