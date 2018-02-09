---
title: "Close 方法 (ADO MD) |Microsoft 文件"
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
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0607ee2889b32906968a5948138191d1fc67bb4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="close-method-ado-md"></a>Close 方法 (ADO MD)
關閉開啟的資料格集。  
  
## <a name="syntax"></a>語法  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>備註  
 使用**關閉**方法，關閉[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件就會在釋放相關聯的資料，包括任何相關資料[儲存格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)，[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)，或[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件。 關閉**資料格集**不會移除它從記憶體中; 您可以變更其屬性設定，稍後重新開啟它。 若要完全消除從記憶體物件，設定為物件變數**Nothing**。  
  
 您可以稍後呼叫[開啟](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法，以重新開啟**資料格集**使用相同或不同來源字串。 雖然**資料格集**物件已關閉，擷取任何屬性或呼叫參考的基礎資料的任何方法或中繼資料會產生錯誤。  
  
## <a name="applies-to"></a>適用於  
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [軸物件 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [資料格物件 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [成員物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [位置物件 (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State 屬性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
