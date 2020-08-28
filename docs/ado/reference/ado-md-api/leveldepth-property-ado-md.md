---
description: LevelDepth 屬性 (ADO MD)
title: LevelDepth 屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- LevelDepth
- Member::LevelDepth
helpviewer_keywords:
- LevelDepth property [ADO MD]
ms.assetid: 8a1cfe2c-f207-4445-b152-ade090f64608
author: rothja
ms.author: jroth
ms.openlocfilehash: 2c21b038df300a5c941d01ba65fdc7240d55c32f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986489"
---
# <a name="leveldepth-property-ado-md"></a>LevelDepth 屬性 (ADO MD)
指出階層的根和 [成員](./member-object-ado-md.md)之間的層級數目。  
  
## <a name="return-values"></a>傳回值  
 傳回 **長** 整數，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 您可以使用 **LevelDepth** 屬性來判斷 [成員](./member-object-ado-md.md)物件與階層根層級之間的距離。 根層級的成員 **LevelDepth**是0。 這會對應至[層級](./level-object-ado-md.md)物件的[Depth](./depth-property-ado-md.md)屬性。  
  
## <a name="applies-to"></a>套用至  
 [Member 物件 (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [深度屬性 (ADO MD) ](./depth-property-ado-md.md)   
 [Level 物件 (ADO MD)](./level-object-ado-md.md)