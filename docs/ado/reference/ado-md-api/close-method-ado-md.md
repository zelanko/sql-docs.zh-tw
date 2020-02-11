---
title: Close 方法（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09e83fd8645a5c0ab604a640478c4cced4870742
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949816"
---
# <a name="close-method-ado-md"></a>Close 方法 (ADO MD)
關閉開啟的儲存格集。  
  
## <a name="syntax"></a>語法  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>備註  
 使用**close**方法關閉資料[格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件將會釋出相關聯的資料，包括任何相關[儲存格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)、[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)、[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)或[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件中的資料。 關閉一個**儲存格**並不會從記憶體中移除它。您可以變更其屬性設定，稍後再重新開啟它。 若要完全排除記憶體中的物件，請將物件變數設為 [**無**]。  
  
 您稍後可以呼叫[Open](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法，使用相同或另一個來源字串重新開啟該**集**。 當資料**格集**物件關閉時，抓取任何屬性或呼叫參考基礎資料或中繼資料的任何方法都會產生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [Axis 物件（ADO MD）](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Cell 物件（ADO MD）](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [成員物件（ADO MD）](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Open 方法（ADO MD）](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [Position 物件（ADO MD）](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State 屬性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
