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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9199563f2a5d6ce594b88577cfb69766cf311492
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765529"
---
# <a name="eos-property"></a>EOS 屬性
指出目前的位置是否在[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)的結尾。  
  
## <a name="return-values"></a>傳回值  
 傳回**布林**值，指出目前的位置是否在資料流程的結尾。 如果資料流程中的位元組數不多，則**EOS**會傳回**True** ;如果在目前位置之後有多個位元組，則會傳回**False** 。  
  
 若要設定資料流程位置的結尾，請使用[SetEOS](../../../ado/reference/ado-api/seteos-method.md)方法。 若要判斷目前的位置，請使用[position](../../../ado/reference/ado-api/position-property-ado.md)屬性。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [EOS 和 LineSeparator 屬性和 SkipLine 方法範例（VB）](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
