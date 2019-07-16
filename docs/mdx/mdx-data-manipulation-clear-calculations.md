---
title: CLEAR CALCULATIONS 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1b0766cb002960a96d702184ac9719abe7610afd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938026"
---
# <a name="mdx-data-manipulation---clear-calculations"></a>MDX 資料操作 - CLEAR CALCULATIONS


  移除 Cube 的所有計算，並使 Cube 回到計算行程 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Expression*  
 有效的多維度運算式 (MDX) Cube 運算式。  
  
## <a name="remarks"></a>備註  
 **FROM**已知，例如，MDX 指令碼在 cube 的內容時，就可以省略子句。  
  
> [!NOTE]  
>  伺服器或資料庫管理員，或可存取 Cube 來源資料的角色成員 (即 ReadSourceData=true) 才能執行這個陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 資料操作陳述式&#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
