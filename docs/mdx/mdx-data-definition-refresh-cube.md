---
title: "REFRESH CUBE 陳述式 (MDX) |Microsoft 文件"
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
- Cube
- REFRESH CUBE
- REFRESH_CUBE
- REFRESH
dev_langs:
- kbMDX
helpviewer_keywords:
- cubes [Analysis Services], cache
- refreshing cache
- REFRESH CUBE statement
- cache [Analysis Services]
ms.assetid: b8c087fb-5d17-4b13-b7cf-9929e9aab35c
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ce57b2384e8cf28dae218dec5f09b756b8cd61c6
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---refresh-cube"></a>重新整理 CUBE 的 MDX 資料定義
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>另請參閱  
 [MDX 資料定義陳述式 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

