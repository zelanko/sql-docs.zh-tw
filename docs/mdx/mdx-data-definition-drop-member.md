---
title: DROP MEMBER 語句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e8e38a3ff3f40f44c911a277f99ab9b629c7c87
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68038190"
---
# <a name="mdx-data-definition---drop-member"></a>MDX 資料定義 - DROP MEMBER


  移除導出成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP MEMBER   
   CURRENTCUBE | Cube_Name  
      .Member_Name   
               [,CURRENTCUBE | Cube_Name.Member_Name ...n]  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供 Cube 名稱的有效字串運算式。  
  
 *Member_Identifier*  
 提供成員名稱或成員索引鍵的有效字串運算式。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;MDX&#41;的 CREATE MEMBER 語句](../mdx/mdx-data-definition-create-member.md)   
 [Mdx 資料定義語句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
