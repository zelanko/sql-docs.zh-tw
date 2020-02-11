---
title: Source 屬性（ADO Error） |Microsoft Docs
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
ms.openlocfilehash: 6b55ebbe5a167b7d70cf606fc4e37e7ede36b486
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67916908"
---
# <a name="source-property-ado-error"></a>Source 屬性 (ADO Error)
表示原本產生錯誤之物件或應用程式的名稱。  
  
## <a name="return-value"></a>傳回值  
 傳回**字串**值，表示物件或應用程式的名稱。  
  
## <a name="remarks"></a>備註  
 使用[錯誤](../../../ado/reference/ado-api/error-object.md)物件的**Source**屬性，來判斷原本產生錯誤之物件或應用程式的名稱。 這可能是物件的類別名稱或程式設計識別碼。 若為 ADO 中的錯誤，屬性值將會是**ADODB。**_Objectname_，其中*objectname*是觸發錯誤的物件名稱。 若為 ADOX 和 ADO MD，此值會是**ADOX。**_ObjectName_和**ADOMD。**_ObjectName_，分別是。  
  
 根據錯誤物件的**來源**、[數目](../../../ado/reference/ado-api/number-property-ado.md)和[描述](../../../ado/reference/ado-api/description-property.md)屬性中的錯誤檔，您可以撰寫程式碼來適當地**處理錯誤。**  
  
 **Error**物件的**Source**屬性是唯讀的。  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、內容説明、NativeError、Number、Source 和 SQLState 屬性範例（VB）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpCoNtext、內容説明、NativeError、Number、Source 和 SQLState 屬性範例（VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 屬性](../../../ado/reference/ado-api/description-property.md)   
 [HelpCoNtext，內容説明的屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 屬性（ADO）](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 屬性（ADO Record）](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Source 屬性 (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
