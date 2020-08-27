---
title: Description 屬性 |Microsoft Docs
description: 瞭解 ADO 中 Error 物件的 description 屬性，此屬性會傳回包含錯誤描述的字串值。
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7060810eba49ad5e1b9385a090788690b43e07eb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973909"
---
# <a name="description-property"></a>Description 屬性
描述 [Error](../../../ado/reference/ado-api/error-object.md) 物件。  
  
## <a name="return-value"></a>傳回值  
 傳回包含錯誤描述的 **字串** 值。  
  
## <a name="remarks"></a>備註  
 使用 **Description** 屬性來取得錯誤的簡短描述。 顯示此屬性，以警告使用者您無法或不想要處理的錯誤。 字串會來自 ADO 或提供者。  
  
 提供者負責將特定的錯誤文字傳遞給 ADO。 ADO 會為每個提供者錯誤或收到的警告，將 [錯誤](../../../ado/reference/ado-api/error-object.md) 物件新增至 **錯誤** 集合。 列舉 **錯誤** 集合，以追蹤提供者所傳遞的錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、NativeError、Number、Source 和 SQLState 屬性範例 (VB) ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [ (VC + +) 的 Description、HelpCoNtext、説明、NativeError、Number、Source 和 SQLState 屬性範例 ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpCoNtext，內容説明屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 屬性 (ADO) ](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 屬性 (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
