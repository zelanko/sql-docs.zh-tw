---
title: Members （字串） (MDX) |Microsoft 文件
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
- Members
dev_langs:
- kbMDX
helpviewer_keywords:
- Members function
ms.assetid: 21fca354-448b-4b05-93f4-111bde1568f1
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9fe851d1ac58e70b8a14212ee8cd8acd3feaf08a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="members-string-mdx"></a>Members (字串) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回由字串運算式指定的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Name*  
 指定成員名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 **Members （字串）**函式會傳回其名稱指定的單一成員。 通常，您會使用**Members （字串）**函數搭配外部函數，提供給**Members （字串）**函式識別成員的字串和**Members （字串）**指定此成員函式傳回的值。  
  
## <a name="example"></a>範例  
 下列範例會使用**Members （字串）**函式，將指定的字串轉換成有效的成員，並傳回字串中指定成員的預設量值。 指定的字串前後要加上單引號。 預設量值是「轉售商銷售數量」量值。  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
