---
title: "DROP CELL CALCULATION 陳述式 (MDX) |Microsoft 文件"
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
- Calculation
- DROP
- DROP_CELL_CALCULATION
- CELL CALCULATION
- DROP CELL
- cell
- DROP CELL CALCULATION
dev_langs:
- kbMDX
helpviewer_keywords:
- deleting calculations
- dropping calculations
- removing calculations
- DROP CELL CALCULATION statement
- calculations [SQL Server]
- cubes [Analysis Services], calculations
ms.assetid: 77caedf4-dd96-4eac-a5e4-fd82148a44a7
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 90e2502709f15620330c69231b590130e1d0cca1
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---drop-cell-calculation"></a>MDX 資料定義卸除的資料格計算
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除指定的資料格計算。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP [ SESSION ] CELL CALCULATION CURRENTCUBE | Cube_Name.CellCalc_Name  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供 Cube 運算式名稱的有效字串運算式。  
  
 *CellCalc_Name*  
 提供所要卸除之資料格計算名稱的有效字串運算式。  
  
## <a name="see-also"></a>另請參閱  
 [建立 CELL CALCULATION 陳述式 &#40;MDX &#41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [MDX 資料定義陳述式 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

