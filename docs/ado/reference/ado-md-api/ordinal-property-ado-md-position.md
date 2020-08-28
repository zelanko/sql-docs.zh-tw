---
description: Ordinal 屬性 (ADO MD Position)
title: 序數屬性 (ADO MD 位置) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Position::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: 6efe8b5d-a2d5-43a9-a5ea-f9244f8d4ec9
author: rothja
ms.author: jroth
ms.openlocfilehash: 6d2485e8331a3eee95cfd5937ffbdbd570b2ecdc
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986189"
---
# <a name="ordinal-property-ado-md-position"></a>Ordinal 屬性 (ADO MD Position)
可唯一識別沿著軸的 [位置](./position-object-ado-md.md) 。  
  
## <a name="return-values"></a>傳回值  
 傳回 **長** 整數，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 [Position](./position-object-ado-md.md)物件的**序數**屬性會對應到[位置集合中](./positions-collection-ado-md.md)的**位置**索引。  
  
 您可以使用每個軸的位置**序數**以及資料**Position**格[集](./cellset-object-ado-md.md)物件的[Item](./item-property-ado-md-cellset.md)屬性，快速抓取資料格。  
  
## <a name="applies-to"></a>套用至  
 [Position 物件 (ADO MD)](./position-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO MD) 的儲存格集物件 ](./cellset-object-ado-md.md)   
 [專案屬性 (ADO MD 格集) ](./item-property-ado-md-cellset.md)   
 [Ordinal 屬性 (ADO MD Cell)](./ordinal-property-ado-md-cell.md)