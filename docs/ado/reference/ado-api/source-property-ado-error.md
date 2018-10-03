---
title: 來源屬性 (ADO Error) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords:
- Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50294b936f211b3a841deb57e55b53f0994517a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611582"
---
# <a name="source-property-ado-error"></a>Source 屬性 (ADO Error)
表示物件或最初產生錯誤的應用程式的名稱。  
  
## <a name="return-value"></a>傳回值  
 傳回**字串**值，指出物件或應用程式的名稱。  
  
## <a name="remarks"></a>備註  
 使用**來源**屬性上的[錯誤](../../../ado/reference/ado-api/error-object.md)物件來判斷最初產生錯誤的應用程式之物件的名稱。 這可能是物件的類別名稱或程式設計識別碼。 在 ADO 中的錯誤，此屬性值會是 **ADODB。 * * * ObjectName*，其中*ObjectName*觸發錯誤的物件名稱。 ADOX 和 ADO MD，此值會是 **ADOX。 * * * ObjectName*和 **ADOMD。 * * * ObjectName，* 分別。  
  
 根據的錯誤說明文件**來源**，[數目](../../../ado/reference/ado-api/number-property-ado.md)，並[描述](../../../ado/reference/ado-api/description-property.md)屬性**錯誤**物件時，您可以撰寫程式碼會適當地處理錯誤。  
  
 **來源**屬性是唯讀**錯誤**物件。  
  
## <a name="applies-to"></a>適用於  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 屬性](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext、 HelpFile 屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 屬性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [來源屬性 （ADO 記錄）](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Source 屬性 (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
