---
title: LineSeparator 屬性（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9248dcabb4c52ceceb6e4876b034480415e77963
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82754812"
---
# <a name="lineseparator-property-ado"></a>LineSeparator 屬性 (ADO)
表示要在文字[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件中當做行分隔符號使用的二進位字元。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)值，指出**資料流程**中使用的行分隔符號字元。 預設值為**adCRLF**。  
  
## <a name="remarks"></a>備註  
 **LineSeparator**是在讀取文字**資料流程**的內容時用來解讀行。 您可以使用[SkipLine](../../../ado/reference/ado-api/skipline-method.md)方法略過這幾行。  
  
 **LineSeparator**僅適用于文字**資料流程**物件（[類型](../../../ado/reference/ado-api/type-property-ado-stream.md)為**adTypeText**）。 如果**類型**為**adTypeBinary**，則會忽略這個屬性。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
