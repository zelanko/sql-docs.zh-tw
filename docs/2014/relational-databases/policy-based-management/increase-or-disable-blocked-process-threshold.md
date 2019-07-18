---
title: 增加或停用已封鎖的處理序閾值 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 71db8ef6-341b-4465-99db-5c63e48d4c7d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 694c5676a5d55fe4fca227d9042ff4f1a9e9d618
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62704970"
---
# <a name="increase-or-disable-blocked-process-threshold"></a>增加或停用 Blocked Process Threshold
  此規則會檢查 blocked process threshold 選項設定為 0 (已停用) 還是設定為高於或等於 5 (秒) 的值。 將 blocked process threshold 選項設定為 1 到 4 的值會造成死結監視器不斷執行。 1 到 4 之間的值應該只用於疑難排解，絕不能在沒有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客戶服務與支援中心協助的情形下，長期使用或用在實際執行環境。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 若要解決這個問題，請將 blocked process threshold 選項設定為 5 (秒) 或更高的值，或是將此值設定為 0 來停用 blocked process threshold。 若要將 blocked process threshold 設定為 `5` 秒的值，請執行以下陳述式：  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 5 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="for-more-information"></a>詳細資訊  
 [已封鎖的處理序臨界值伺服器組態選項](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
