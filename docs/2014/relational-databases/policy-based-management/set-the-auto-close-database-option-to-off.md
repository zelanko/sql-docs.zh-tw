---
title: 將 AUTO_CLOSE 資料庫選項設定為 OFF | Microsoft Docs
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
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0b84816146ebd801239301693934cbf73141cad9
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43816424"
---
# <a name="set-the-autoclose-database-option-to-off"></a>將 AUTO_CLOSE 資料庫選項設定為 OFF
  這個規則會檢查 AUTO_ CLOSE 選項是否設定為 OFF。 當 AUTO_CLOSE 設定為 ON 時，這個選項可能會造成經常存取之資料庫的效能降低，因為在每一個連接之後都會增加開啟和關閉資料庫的負擔。 在每一個連接之後，AUTO_CLOSE 也會排清程序快取。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 如果經常存取資料庫，請將此資料庫的 AUTO_CLOSE 選項設定為 OFF。  
  
## <a name="for-more-information"></a>詳細資訊  
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
