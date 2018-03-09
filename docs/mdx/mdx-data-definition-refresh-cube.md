---
title: "REFRESH CUBE 陳述式 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Cube
- REFRESH CUBE
- REFRESH_CUBE
- REFRESH
dev_langs: kbMDX
helpviewer_keywords:
- cubes [Analysis Services], cache
- refreshing cache
- REFRESH CUBE statement
- cache [Analysis Services]
ms.assetid: b8c087fb-5d17-4b13-b7cf-9929e9aab35c
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 37649d37d1cef67eb50caf8f3768beba19545988
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-definition---refresh-cube"></a>重新整理 CUBE 的 MDX 資料定義
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  重新整理 Cube 的用戶端快取。  
  
## <a name="syntax"></a>語法  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供 Cube 名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 用戶端應用程式連接到的執行個體[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，此陳述式會導致用戶端應用程式與伺服器同步快取的記憶體。 上述動作一般會自動偵測和更新，但發生前的時間長短相依於用戶端連接字串設定。 REFRESH CUBE 陳述式會立即重新整理資料。  
  
 對於連接到本機 Cube 的用戶端應用程式，REFRESH CUBE 陳述式會重建本機 Cube 檔案。  
  
> [!IMPORTANT]  
>  不會重新整理伺服器上儲存的命名集。  
  
## <a name="see-also"></a>請參閱  
 [MDX 資料定義陳述式 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
