---
title: LineSeparator 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b55f82e92ff74ba359074613205bc8086af81b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864452"
---
# <a name="lineseparator-property-ado"></a>LineSeparator 屬性 (ADO)
表示為文字行分隔符號要使用的二進位字元[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)值，指出所用的行分隔符號字元**Stream**。 預設值是**adCRLF**。  
  
## <a name="remarks"></a>備註  
 **LineSeparator**用來讀取的文字內容時，解譯線條**Stream**。 可以略過行，與[SkipLine](../../../ado/reference/ado-api/skipline-method.md)方法。  
  
 **LineSeparator**僅適用於文字**Stream**物件 ([類型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 如果此屬性則會忽略**型別**是**adTypeBinary**。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
