---
title: REFRESH CUBE 語句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 957609573c206b7c3492789c369d0fb2be2398a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038158"
---
# <a name="mdx-data-definition---refresh-cube"></a>MDX 資料定義 - REFRESH CUBE


  重新整理 Cube 的用戶端快取。  
  
## <a name="syntax"></a>語法  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供 Cube 名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 若為連接到實例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]用戶端應用程式，此語句會導致用戶端應用程式上快取的記憶體與伺服器同步。 上述動作一般會自動偵測和更新，但發生前的時間長短相依於用戶端連接字串設定。 REFRESH CUBE 陳述式會立即重新整理資料。  
  
 對於連接到本機 Cube 的用戶端應用程式，REFRESH CUBE 陳述式會重建本機 Cube 檔案。  
  
> [!IMPORTANT]  
>  不會重新整理伺服器上儲存的命名集。  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 資料定義語句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
