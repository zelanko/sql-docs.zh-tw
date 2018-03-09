---
title: "LineSeparator 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3742653b10e98c7608557da86a2975b24e472b9c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="lineseparator-property-ado"></a>LineSeparator 屬性 (ADO)
表示為文字行分隔符號使用的二進位字元[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)值，指出使用中的行分隔字元**資料流**。 預設值是**adCRLF**。  
  
## <a name="remarks"></a>備註  
 **LineSeparator**用來讀取的文字內容時，解譯行**資料流**。 行可以與已略過[SkipLine](../../../ado/reference/ado-api/skipline-method.md)方法。  
  
 **LineSeparator**僅適用於文字**資料流**物件 ([類型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 如果這個屬性就會忽略**類型**是**adTypeBinary**。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
