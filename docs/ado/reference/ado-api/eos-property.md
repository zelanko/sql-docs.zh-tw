---
title: EOS 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords:
- EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47b3e48e612e0ee5595ada33127f016ee6b986f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47650668"
---
# <a name="eos-property"></a>EOS 屬性
表示目前位置是否在結尾[資料流](../../../ado/reference/ado-api/stream-object-ado.md)。  
  
## <a name="return-values"></a>傳回值  
 傳回**布林**值，指出目前的位置是否位於資料流結尾。 **EOS**會傳回 **，則為 True**有沒有更多的位元組資料流; 它會傳回**False**如果有多個位元組，遵循目前的位置。  
  
 若要設定資料流位置的結尾，請使用[SetEOS](../../../ado/reference/ado-api/seteos-method.md)方法。 若要判斷目前的位置，請使用[位置](../../../ado/reference/ado-api/position-property-ado.md)屬性。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [EOS 和 LineSeparator 屬性和 SkipLine 方法範例 (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
