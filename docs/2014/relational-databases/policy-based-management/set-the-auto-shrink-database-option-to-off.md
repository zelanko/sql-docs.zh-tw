---
title: 將 AUTO_SHRINK 資料庫選項設定為 OFF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b15056560796048835e0f54dad783f9e3b01b0fb
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43819134"
---
# <a name="set-the-autoshrink-database-option-to-off"></a>將 AUTO_SHRINK 資料庫選項設定為 OFF
  這個規則會檢查 AUTO_SHRINK 資料庫選項是否設定為 OFF。 通常壓縮和展開資料庫可能會導致實體片段。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 將 AUTO_SHRINK 資料庫選項設定為 OFF。 如果您知道您所回收的空間不需要在將來使用，您可以手動壓縮資料庫來回收該空間。  
  
## <a name="for-more-information"></a>詳細資訊  
 Microsoft 知識庫文件 [315512](http://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
