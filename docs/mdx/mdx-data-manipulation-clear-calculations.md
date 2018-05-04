---
title: CLEAR CALCULATIONS 陳述式 (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CLEAR CALCULATIONS
- clalculations
- clear
dev_langs:
- kbMDX
helpviewer_keywords:
- clearing calculations
- CLEAR CALCULATIONS statement
- deleting calculations
- removing calculations
- calculations [Analysis Services], clearing
- cubes [Analysis Services], calculations
ms.assetid: aebec9a1-1d1d-4697-aa3f-cc2449625603
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 84cfc46ea64b0d4fb1dd79532bc6bdba9af71ded
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-manipulation---clear-calculations"></a>MDX 資料操作 CLEAR CALCULATIONS
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  移除 Cube 的所有計算，並使 Cube 回到計算行程 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Expression*  
 有效的多維度運算式 (MDX) Cube 運算式。  
  
## <a name="remarks"></a>備註  
 **FROM**已知，例如 MDX 指令碼在 cube 的內容時，就可以省略子句。  
  
> [!NOTE]  
>  伺服器或資料庫管理員，或可存取 Cube 來源資料的角色成員 (即 ReadSourceData=true) 才能執行這個陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 資料操作陳述式&#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
