---
title: "錯誤 (MDX) |Microsoft 文件"
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
- ERROR
dev_langs:
- kbMDX
helpviewer_keywords:
- Error function
ms.assetid: 2caac19b-b297-443e-9299-648ef88a5039
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b439b8b6d6c36cf500ad5f089a24034e7d2404fb
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="error-mdx"></a>Error (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  引發錯誤，選擇性提供指定的錯誤訊息。  
  
## <a name="syntax"></a>語法  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>引數  
 *Error_Text*  
 包含要傳回之錯誤訊息的有效字串運算式。  
  
## <a name="examples"></a>範例  
 下列查詢會示範如何使用**錯誤**函式內的導出量值：  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

