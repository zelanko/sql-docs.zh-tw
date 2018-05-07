---
title: CALL 陳述式 (MDX) |Microsoft 文件
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
f1_keywords:
- CALL
dev_langs:
- kbMDX
helpviewer_keywords:
- voids [MDX]
- stored procedures [MDX]
- CALL statement
ms.assetid: b534a20b-924c-43b8-832d-24e57d50425c
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 079f29676bd1f71d70e182af2ee8664361916d49
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-manipulation---call"></a>MDX 資料操作呼叫
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在目前範圍中或選擇性在指定 Cube 上，執行會傳回空值的預存程序。  
  
## <a name="syntax"></a>語法  
  
```  
  
CALL SP_Name   
   [ (SP_Argument   
      [, SP_Argument ,...n]  
      ) ]   
[ONCube_Expression]  
```  
  
## <a name="arguments"></a>引數  
 *SP_Name*  
 提供預存程序名稱的有效字串運算式。  
  
 *SP_Argument*  
 提供引數給被呼叫之預存程序的有效字串運算式。  
  
 *Cube_Expression*  
 提供 Cube 名稱的有效字串 Cube 運算式。  
  
## <a name="remarks"></a>備註  
 **呼叫**陳述式會執行指定已註冊預存程序，並選擇性地包含一或多個引數指定的預存程序。 **呼叫**陳述式會傳回空值的預存程序只能搭配使用。 此陳述式無法與 MDX 運算式內的其他函數或運算子組合。 傳回值的已註冊預存程序可以直接在 MDX 運算式內呼叫，而且可與其他 MDX 函數與運算子組合。  
  
 如果沒有指定 Cube，陳述式會在目前 Cube 上執行預存程序。  
  
> [!NOTE]  
>  如果預存程序未登錄在用戶端，**呼叫**陳述式嘗試呼叫預存程序的執行個體從[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 資料操作陳述式&#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [使用預存程序 &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)  
  
  
