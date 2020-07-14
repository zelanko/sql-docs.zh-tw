---
title: " ADR 清除工具重試逾時 (分) 組態選項 | Microsoft Docs"
description: 說明適用於 ADR 清除工具重試逾時的 SQL Server 執行個體組態設定。
ms.custom: ''
ms.date: 06/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ADR cleaner retry timeout (min)
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 25d7df032b0606a324d98d14258cbbd40602bae7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85698162"
---
# <a name="adr-cleaner-retry-timeout-min-configuration-option"></a>ADR 清除工具重試逾時 (分) 組態選項

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

已在 SQL Server 2019 中導入。

這是[加速資料庫復原](../../relational-databases/accelerated-database-recovery-concepts.md)所需的組態設定。 清除工具是一種非同步處理序，會定期喚醒並清理不需要的分頁版本。

清除工具偶爾會因為在清理期間與使用者工作負載發生衝突，而在取得物件層級鎖定時遇到問題。 其會在個別清單中追蹤這類頁面。 ADR 清除工具重試逾時 (預設值為 15) 會控制清除工具在放棄清理之前，獨佔重試物件鎖定取得和清除頁面所花費的時間量。 完成 100% 成功的清理，在中止的交易對應中維持中止交易的成長，是不可或缺的。 如果無法在指定的逾時內清除個別清單，則將放棄目前的清理，並啟動下一個清理。

## <a name="remarks"></a>備註  

此清除工具為 SQL Server 2019 中的單一執行緒，因此，一個 SQL Server 執行個體一次只能在一個資料庫上運作。 如果執行個體具有多個已啟用 ADR 的使用者資料庫，則不會將逾時提高為較大的值，因為，那樣可能會在某個資料庫上進行重試時延遲另一個資料庫上的清除。

## <a name="examples"></a>範例

下列範例會設定清除工具重試逾時。

```tsql
sp_configure 'show advanced options', 1;  
RECONFIGURE;
GO 
sp_configure 'ADR cleaner retry timeout', 15;  
RECONFIGURE;  
GO  
```  

## <a name="see-also"></a>另請參閱  

- [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [加速資料庫復原](../../relational-databases/accelerated-database-recovery-concepts.md)
- [管理加速資料庫復原](../../relational-databases/accelerated-database-recovery-management.md)