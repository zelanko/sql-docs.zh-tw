---
title: 保留鎖定組態選項預設值 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: f214f05b-5f0b-4786-b2ad-b8b4b6e58d72
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a45e9b7cb639b0588750fc9b2a9b70a25cd7f0f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63057964"
---
# <a name="keep-the-locks-configuration-option-default-value"></a>保留鎖定組態選項預設值
  此規則會檢查 locks configuration 選項的值。 這個選項會判斷可用鎖定數目的最大值。 這會限制 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 用於鎖定的記憶體數量。 預設值 0 會讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 根據變更的系統需求，動態配置及取消配置鎖定結構。  
  
 如果鎖定是非零的值，批次作業將會停止，而且如果超過指定的值，將會產生「鎖定不足」的錯誤訊息。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 使用 sp_configure 系統預存程序，可透過以下陳述式將鎖定的值變更為它的預設值：  
  
```  
EXEC sp_configure 'locks', 0;  
```  
  
## <a name="for-more-information"></a>詳細資訊  
 [設定 locks 伺服器組態選項](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md)  
  
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql)  
  
 [Microsoft 知識庫文章 271509](https://go.microsoft.com/fwlink/?linkid=117788)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
