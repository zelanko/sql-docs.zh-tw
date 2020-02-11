---
title: Description 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords:
- Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 48b3a6987e6c7b6c3754f5041d90d248520345ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933082"
---
# <a name="description-property"></a>Description 屬性
描述[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回包含錯誤描述的**字串**值。  
  
## <a name="remarks"></a>備註  
 使用**Description**屬性來取得錯誤的簡短描述。 顯示此屬性，以警示使用者您無法或不想要處理的錯誤。 此字串會來自 ADO 或提供者。  
  
 提供者會負責將特定的錯誤文字傳遞給 ADO。 ADO 會針對每個提供者錯誤或收到的警告，將[錯誤](../../../ado/reference/ado-api/error-object.md)物件加入至**錯誤**集合。 列舉**錯誤**集合，以追蹤提供者所傳遞的錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、內容説明、NativeError、Number、Source 和 SQLState 屬性範例（VB）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpCoNtext、內容説明、NativeError、Number、Source 和 SQLState 屬性範例（VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpCoNtext，內容説明的屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 屬性（ADO）](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 屬性 (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
