---
title: DROP MEMBER 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 78d5d27853922d7e7524d93ae2b8157e57166968
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248285"
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
 [CREATE MEMBER 陳述式 &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [MDX 資料定義陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
