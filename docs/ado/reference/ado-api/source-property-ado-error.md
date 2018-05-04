---
title: 來源屬性 （ADO 錯誤） |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords:
- Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1db468ae4575a494b03efc5cf9eb3372b6d5cab2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="source-property-ado-error"></a>來源屬性 （ADO 錯誤）
表示原始產生錯誤的應用程式之物件的名稱。  
  
## <a name="return-value"></a>傳回值  
 傳回**字串**值，指出物件或應用程式的名稱。  
  
## <a name="remarks"></a>備註  
 使用**來源**屬性[錯誤](../../../ado/reference/ado-api/error-object.md)物件，以判斷原始產生錯誤的應用程式之物件的名稱。 這可能是物件的類別名稱或程式設計識別碼。 屬性值將會在 ADO 中的錯誤，**ADODB。 * * * ObjectName*，其中*ObjectName*觸發錯誤之物件的名稱。 ADOX 和 ADO MD 中，值會是 **ADOX。 * * * ObjectName*和 **ADOMD。 * * * ObjectName，*分別。  
  
 根據的錯誤說明文件**來源**，[數目](../../../ado/reference/ado-api/number-property-ado.md)，和[描述](../../../ado/reference/ado-api/description-property.md)屬性**錯誤**物件，您可以撰寫程式碼會適當地處理錯誤。  
  
 **來源**屬性是唯讀，如**錯誤**物件。  
  
## <a name="applies-to"></a>適用於  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [描述、 HelpContext、 說明檔案、 NativeError、 數字、 來源和 SQLState 屬性範例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 說明檔案、 NativeError、 數字、 來源和 SQLState 屬性範例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 屬性](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext，HelpFile 屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 屬性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [來源屬性 （ADO 資料錄）](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Source 屬性 (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
