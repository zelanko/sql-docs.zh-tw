---
title: "EOS 屬性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords: EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf26c00ecf445c9354d20fa5878942b56f2d2d19
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="eos-property"></a>EOS 屬性
指出目前位置是否在結尾[資料流](../../../ado/reference/ado-api/stream-object-ado.md)。  
  
## <a name="return-values"></a>傳回值  
 傳回**布林**值，指出目前的位置是否位於資料流結尾。 **EOS**傳回**True**有沒有更多的位元組資料流; 它會傳回**False**如果有多個位元組之後的目前位置。  
  
 若要設定資料流位置的結尾，使用[SetEOS](../../../ado/reference/ado-api/seteos-method.md)方法。 若要判斷目前的位置，請使用[位置](../../../ado/reference/ado-api/position-property-ado.md)屬性。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>請參閱  
 [EOS 和 LineSeparator 屬性 SkipLine 方法範例 (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
