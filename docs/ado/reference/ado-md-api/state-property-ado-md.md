---
title: 狀態屬性 (ADO MD) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1960818e3ebf5b58610e18bfb23ee7c8c3101b8e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="state-property-ado-md"></a>State 屬性 (ADO MD)
表示資料格集的目前狀態。  
  
## <a name="return-values"></a>傳回值  
 傳回**長**整數，指出目前的狀況[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件，並為唯讀。 下列是有效值： **adStateClosed** (0) 和**adStateOpen** (1)。  
  
## <a name="remarks"></a>備註  
 若要使用[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)常數的名稱，您必須在專案中參考的 ADO 類型程式庫。 請參閱[使用 ADO 與 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)如需詳細資訊。  
  
## <a name="applies-to"></a>適用於  
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [Close 方法 (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
