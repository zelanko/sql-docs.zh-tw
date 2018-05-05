---
title: MDX 資料定義陳述式 (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- MDX [Analysis Services], data manipulation
- data manipulation [MDX]
- data definition statements [MDX]
- Multidimensional Expressions [Analysis Services], data manipulation
ms.assetid: 1f975d7f-8875-43b6-a571-9d5cd7c70217
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 84a173a4e3496d61f8f1b1fc837908d2706af5b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition-statements-mdx"></a>MDX 資料定義陳述式 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在多維度運算式 (MDX) 中，資料定義陳述式可建立、卸除和管理多維度物件。 下表列出可用的資料定義陳述式。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[ALTER CUBE 陳述式 & #40;MDX & #41;](../mdx/mdx-data-definition-alter-cube.md)|改變指定 Cube 的結構。|  
|[CREATE ACTION 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-create-action.md)|建立與 Cube、維度、階層或從屬物件關聯的動作。|  
|[建立 CELL CALCULATION 陳述式 & #40;MDX & #41;](../mdx/mdx-data-definition-create-cell-calculation.md)|在 Cube 內指定的 Tuple 集合上，建立評估 MDX 運算式的計算。|  
|[CREATE GLOBAL CUBE 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-create-global-cube.md)|根據伺服器上 Cube 的 Subcube，建立和擴展本機保存的 Cube。 連接到本機保存的 Cube 不需要連接伺服器。|  
|[建立 MEMBER 陳述式 & #40;MDX & #41;](../mdx/mdx-data-definition-create-member.md)|建立導出成員。|  
|[CREATE SESSION CUBE 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-create-session-cube.md)|根據伺服器上的 Cube，建立並擴展可供同一工作階段中所有查詢使用的 Cube。|  
|[建立 SET 陳述式 & #40;MDX & #41;](../mdx/mdx-data-definition-create-set.md)|建立指定 Cube 的命名集。|  
|[CREATE SUBCUBE 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-create-subcube.md)|將指定 Cube 或 Subcube 的 Cube 空間重新定義為指定的 Subcube。|  
|[DROP ACTION 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-action.md)|刪除指定 Cube 的指定動作。|  
|[DROP CELL CALCULATION 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md)|移除指定的資料格計算。|  
|[DROP MEMBER 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)|移除導出成員。|  
|[DROP SET 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md)|移除命名集。|  
|[DROP SUBCUBE 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-subcube.md)|卸除指定的 Subcube，還原為先前定義的 Cube 或具有指定名稱的 Subcube 定義。|  
|[重新整理 CUBE 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-refresh-cube.md)|重新整理 Cube 的用戶端快取。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 陳述式參考&#40;MDX&#41;](../mdx/mdx-statement-reference-mdx.md)   
 [MDX 資料操作陳述式&#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [MDX 指令碼陳述式 & #40;MDX & #41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
