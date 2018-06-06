---
title: UserName (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 887af13c84fd06ead5a36564c0dda740a5f6d0b0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581350"
---
# <a name="username-mdx"></a>UserName (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回目前連接的網域名稱與使用者名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>備註  
 所傳回的值是採用下列格式的字串：  
  
 *網域名稱 \ 使用者名稱*  
  
## <a name="example"></a>範例  
 下列範例會傳回執行查詢之使用者的使用者名稱。  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
