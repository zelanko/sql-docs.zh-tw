---
title: 使用者名稱（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f1ebb5dc504b799575b2ccf9e47368e4e6511dac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097267"
---
# <a name="username-mdx"></a>UserName (MDX)


  傳回目前連接的網域名稱與使用者名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>備註  
 所傳回的值是採用下列格式的字串：  
  
 *domain-name\user-name*  
  
## <a name="example"></a>範例  
 下列範例會傳回執行查詢之使用者的使用者名稱。  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
