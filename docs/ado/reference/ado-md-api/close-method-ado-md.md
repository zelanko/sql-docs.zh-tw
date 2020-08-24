---
description: Close 方法 (ADO MD)
title: 關閉方法 (ADO MD) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 666cf9afc4f6f5df5d3e950948e60bd644a45cdb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778267"
---
# <a name="close-method-ado-md"></a>Close 方法 (ADO MD)
關閉開啟的儲存格。  
  
## <a name="syntax"></a>語法  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>備註  
 使用 **close** 方法關閉資料 [格集](./cellset-object-ado-md.md) 物件將會釋放相關聯的資料，包括任何相關資料 [格](./cell-object-ado-md.md)、 [軸](./axis-object-ado-md.md)、 [位置](./position-object-ado-md.md)或 [成員](./member-object-ado-md.md) 物件中的資料。 關閉一 **格集** 並不會將它從記憶體中移除;您可以變更其屬性設定，稍後再重新開啟。 若要完全消除記憶體中的物件，請將物件變數設定為 **Nothing**。  
  
 您稍後可以使用相同或其他來源字串，呼叫 [Open](./open-method-ado-md.md) 方法來重新開啟 **儲存格** 。 當資料 **格集** 物件關閉時，抓取任何屬性或呼叫參考基礎資料或中繼資料的任何方法，都會產生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Cellset 物件 (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [軸物件 (ADO MD) ](./axis-object-ado-md.md)   
 [資料格物件 (ADO MD) ](./cell-object-ado-md.md)   
 [成員物件 (ADO MD) ](./member-object-ado-md.md)   
 [開啟方法 (ADO MD) ](./open-method-ado-md.md)   
 [Position 物件 (ADO MD) ](./position-object-ado-md.md)   
 [State 屬性 (ADO MD)](./state-property-ado-md.md)