---
description: Number 屬性 (ADO)
title: Number 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords:
- number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
author: rothja
ms.author: jroth
ms.openlocfilehash: a44c1a4902dbcd37089ee63c41db2b9a089c3aed
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990429"
---
# <a name="number-property-ado"></a>Number 屬性 (ADO)
指出可唯一識別 [錯誤](./error-object.md) 物件的數位。  
  
## <a name="return-value"></a>傳回值  
 傳回可能對應至其中一個[ErrorValueEnum](./errorvalueenum.md)常數的**Long**值。  
  
## <a name="remarks"></a>備註  
 使用 **Number** 屬性來判斷發生了哪些錯誤。 屬性的值是對應于錯誤條件的唯一數位。  
  
 [Errors](./errors-collection-ado.md)集合會以十六進位格式傳回 HRESULT (例如，0x80004005) 或 long 值 (例如 2147467259) 。 這些 Hresult 可由基礎元件（例如 OLE DB 或甚至是 OLE 本身）引發。 如需這些數位的詳細資訊，請參閱 OLE DB 程式設計[人員參考](/previous-versions/windows/desktop/ms713643(v=vs.85))中的[錯誤 (OLE DB) ](/previous-versions/windows/desktop/ms724533(v=vs.85)) *。*  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](./error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、NativeError、Number、Source 和 SQLState 屬性範例 (VB) ](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [ (VC + +) 的 Description、HelpCoNtext、説明、NativeError、Number、Source 和 SQLState 屬性範例 ](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 屬性](./description-property.md)   
 [HelpCoNtext，內容説明屬性](./helpcontext-helpfile-properties.md)   
 [Source 屬性 (ADO Error)](./source-property-ado-error.md)