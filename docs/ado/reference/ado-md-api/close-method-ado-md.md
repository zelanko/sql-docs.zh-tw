---
title: Close 方法 (ADO MD) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 4f01845752c0ee1f9187ea3d209a97509f87a5a9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709572"
---
# <a name="close-method-ado-md"></a>Close 方法 (ADO MD)
關閉開啟的資料格集。  
  
## <a name="syntax"></a>語法  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>備註  
 使用 **關閉** 方法以關閉[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件會釋放相關聯的資料，包括任何相關的資料[儲存格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)，[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)，或[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件。 關閉**資料格集**不會移除它從記憶體中; 您可以變更其屬性設定，並稍後再重新開啟它。 若要完全排除記憶體中的物件，設定為物件變數**Nothing**。  
  
 您可以於稍後呼叫[開放](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法來重新開啟**資料格集**使用相同或另一個來源字串。 雖然**資料格集**物件已關閉，擷取任何屬性或呼叫任何方法的參考的基礎資料或中繼資料會產生錯誤。  
  
## <a name="applies-to"></a>適用於  
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [Axis 物件 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Cell 物件 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [成員物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [位置物件 (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State 屬性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
