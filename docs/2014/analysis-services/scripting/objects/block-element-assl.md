---
title: 封鎖元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Block Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Block
helpviewer_keywords:
- Block element
ms.assetid: f45c32ae-e4e0-465a-9564-9ccfb10a858f
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e382ba38c41bc68b3d49b0397cdc3fe3f2dcf0ac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131996"
---
# <a name="block-element-assl"></a>Block 元素 (ASSL)
  包含所有或部分二進位內容的[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Blocks>  
   <Block>...</Block>  
</Blocks>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|Base64Binary|  
|預設值|無|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[區塊](../collections/blocks-element-assl.md)|  
|子元素|無|  
  
## <a name="see-also"></a>另請參閱  
 [Assembly 項目&#40;ASSL&#41;](assembly-element-assl.md)   
 [ClrAssembly 資料類型&#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [檔案項目&#40;ASSL&#41;](../collections/files-element-assl.md)   
 [檔案項目&#40;ASSL&#41;](file-element-assl.md)   
 [ClrAssemblyFile 資料類型&#40;ASSL&#41;](../data-type/clrassemblyfile-data-type-assl.md)   
 [資料元素&#40;ASSL&#41;](data-element-assl.md)   
 [DataBlock 資料類型&#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  