---
title: 將 AUTO_SHRINK 資料庫選項設定為 OFF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 42d79ed13a691c3d39a28e7ab35a740a9f613fac
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066680"
---
# <a name="set-the-auto_shrink-database-option-to-off"></a>將 AUTO_SHRINK 資料庫選項設定為 OFF
  這個規則會檢查 AUTO_SHRINK 資料庫選項是否設定為 OFF。 通常壓縮和展開資料庫可能會導致實體片段。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 將 AUTO_SHRINK 資料庫選項設定為 OFF。 如果您知道您所回收的空間不需要在將來使用，您可以手動壓縮資料庫來回收該空間。  
  
## <a name="for-more-information"></a>詳細資訊  
 Microsoft 知識庫文件 [315512](https://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
