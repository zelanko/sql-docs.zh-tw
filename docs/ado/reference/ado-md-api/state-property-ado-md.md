---
description: State 屬性 (ADO MD)
title: 狀態屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
author: rothja
ms.author: jroth
ms.openlocfilehash: 5ef7a26ae4b1f45476fb8074402a84a97d3aace8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440740"
---
# <a name="state-property-ado-md"></a>State 屬性 (ADO MD)
指出儲存格的目前狀態。  
  
## <a name="return-values"></a>傳回值  
 傳回 **長** 整數，指出目前的 [儲存格](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 物件的條件，而且是唯讀的。 下列值有效： **adStateClosed** (0) 和 **adStateOpen** (1) 。  
  
## <a name="remarks"></a>備註  
 若要使用 [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) 常數名稱，您必須在專案中參考 ADO 類型程式庫。 如需詳細資訊，請參閱搭配 [使用 ADO 與 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) 。  
  
## <a name="applies-to"></a>套用至  
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [關閉方法 (ADO MD) ](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
