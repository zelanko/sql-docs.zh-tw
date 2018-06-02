---
title: REFRESH CUBE 陳述式 (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f27051d9e0fe1d0a6eb3d580548233eb9f073215
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579770"
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
  
## <a name="see-also"></a>另請參閱  
 [MDX 資料定義陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
