---
title: 針對特定工作負載最佳化伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7edf279b49374823c9083005be9b8d047b003f62
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640249"
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>針對特定工作負載最佳化伺服器組態選項
  **optimize for ad hoc workloads** 選項是用來針對包含許多使用一次特定批次的工作負載，改善計畫快取的效率。 如果這個選項設定為 1， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會在首次編譯批次時，將小型已編譯計畫虛設常式 (而非完整的已編譯計畫) 儲存在計畫快取中。 這會透過避免計畫快取填滿不重複使用的已編譯計畫，協助減輕記憶體不足的壓力。  
  
 已編譯計畫虛設常式可讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 辨識出這個特定批次先前已經編譯，但是只儲存已編譯計畫虛設常式，如此再次叫用 (編譯或執行) 這個批次時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會編譯此批次、從計畫快取中移除已編譯計畫虛設常式，並且將完整的已編譯計畫加入至計畫快取。  
  
 將 **optimize for ad hoc workloads** 設定為 1 只會影響新的計畫。已經存在計畫快取中的計畫則不會受到影響。  
  
 已編譯計畫虛設常式是 sys.dm_exec_cached_plans 目錄檢視所顯示的其中一個 cacheobjtype。 它具有唯一的 SQL 控制代碼和計畫控制代碼。 已編譯計畫虛設常式沒有相關聯的執行計畫，因此查詢計畫控制代碼將不會傳回 XML 執行程序表。  
  
 追蹤旗標 8032 會將快取限制參數還原為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RTM 設定，這項設定通常會允許使用更大的快取。 當經常重複使用的快取項目無法納入快取中，以及 [針對特定工作負載最佳化伺服器組態選項]  無法解決計畫快取的問題時，請使用這項設定。  
  
> [!WARNING]  
>  如果大型快取為其他記憶體取用者 (例如緩衝集區) 提供較少的記憶體，追蹤旗標 8032 可能會導致效能降低。  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
