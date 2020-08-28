---
description: EOS 屬性
title: EOS 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f7df00678197a4b9d16298e5f680263673fd10e8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973779"
---
# <a name="eos-property"></a>EOS 屬性
指出目前的位置是否在 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md)的結尾。  
  
## <a name="return-values"></a>傳回值  
 傳回 **布林** 值，指出目前的位置是否位於資料流程的結尾。 如果資料流程中沒有其他位元組，則**EOS**會傳回**True** ;如果目前位置之後有更多位元組，則會傳回**False** 。  
  
 若要設定資料流程位置的結尾，請使用 [SetEOS](../../../ado/reference/ado-api/seteos-method.md) 方法。 若要判斷目前的位置，請使用 [position](../../../ado/reference/ado-api/position-property-ado.md) 屬性。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [LineSeparator 屬性和 SkipLine 方法範例 (VB) ](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
