---
title: "CLEAR CALCULATIONS 陳述式 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 042c7b9bedc396d63aa70d23926728b015527a99
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-manipulation---clear-calculations"></a>MDX 資料操作 CLEAR CALCULATIONS
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [MDX 資料操作陳述式 &#40;MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  

