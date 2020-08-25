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
ms.openlocfilehash: efc3b140b2864aec7151e1235010c4a14b0b3a64
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777857"
---
# <a name="state-property-ado-md"></a>State 屬性 (ADO MD)
指出儲存格的目前狀態。  
  
## <a name="return-values"></a>傳回值  
 傳回 **長** 整數，指出目前的 [儲存格](./cellset-object-ado-md.md) 物件的條件，而且是唯讀的。 下列值有效： **adStateClosed** (0) 和 **adStateOpen** (1) 。  
  
## <a name="remarks"></a>備註  
 若要使用 [ObjectStateEnum](../ado-api/objectstateenum.md) 常數名稱，您必須在專案中參考 ADO 類型程式庫。 如需詳細資訊，請參閱搭配 [使用 ADO 與 ADO MD](../../guide/multidimensional/using-ado-with-ado-md.md) 。  
  
## <a name="applies-to"></a>套用至  
 [Cellset 物件 (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [關閉方法 (ADO MD) ](./close-method-ado-md.md)   
 [Open 方法 (ADO MD)](./open-method-ado-md.md)