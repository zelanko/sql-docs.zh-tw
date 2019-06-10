---
title: 針對特定工作負載最佳化伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 90e61107f4f552e6a871c953f0dd5874d42a4a71
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66772306"
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>針對特定工作負載最佳化伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **optimize for ad hoc workloads** 選項是用來針對包含許多使用一次特定批次的工作負載，改善計畫快取的效率。 如果這個選項設定為 1， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會在首次編譯批次時，將小型已編譯計畫虛設常式 (而非完整的已編譯計畫) 儲存在計畫快取中。 這會透過避免計畫快取填滿不重複使用的已編譯計畫，協助減輕記憶體不足的壓力。 
  
  已編譯計畫虛設常式可讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 辨識出這個特定批次先前已經編譯，但是只儲存已編譯計畫虛設常式，如此再次叫用 (編譯或執行) 這個批次時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會編譯此批次、從計畫快取中移除已編譯計畫虛設常式，並且將完整的已編譯計畫加入至計畫快取。 
  
 已編譯計畫虛設常式是 sys.dm_exec_cached_plans 目錄檢視所顯示的其中一個 cacheobjtype。 它具有唯一的 SQL 控制代碼和計畫控制代碼。 已編譯計畫虛設常式沒有相關聯的執行計畫，因此查詢計畫控制代碼將不會傳回 XML 執行程序表。  
  
 [追蹤旗標 8032](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 會將快取限制參數還原為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RTM 設定，這項設定通常會允許使用更大的快取。 當經常重複使用的快取項目無法納入快取中，以及 [針對特定工作負載最佳化伺服器組態選項] 無法解決計畫快取的問題時，請使用這項設定。  
  
> [!WARNING]  
>  如果大型快取為其他記憶體取用者 (例如緩衝集區) 提供較少的記憶體，追蹤旗標 8032 可能會導致效能降低。  

## <a name="recommendations"></a>建議
請避免在計畫快取中有大量的單次使用計畫。 此問題經常是查詢參數的資料類型未一致定義所致。 這特別適用於字串的長度，但可套用至具有長度上限、有效位數或小數位數的任何資料類型。 例如，如果名為 @Greeting 的參數在某次呼叫時作為 Nvarchar(10) 傳遞，並在下次呼叫時作為 Nvarchar(20) 傳遞，則會為每個參數大小建立個別的計畫。 如果查詢具有數個參數，而且其在呼叫時未一致定義，則每個查詢可能存在大量的查詢計畫。 每個曾使用之查詢參數資料類型和長度的組合都可能存在計畫。

如果一次性計畫的數目佔用 OLTP 伺服器中絕大部分的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 記憶體，且這些計畫為特定計畫，請使用此伺服器選項來降低這些物件的記憶體使用量。
若要找到一次性快取計畫的數目，請執行下列查詢：

```sql
SELECT objtype, cacheobjtype, 
  AVG(usecounts) AS Avg_UseCount, 
  SUM(refcounts) AS AllRefObjects, 
  SUM(CAST(size_in_bytes AS bigint))/1024/1024 AS Size_MB
FROM sys.dm_exec_cached_plans
WHERE objtype = 'Adhoc' AND usecounts = 1
GROUP BY objtype, cacheobjtype;
```

> [!IMPORTANT]
> 將 **optimize for ad hoc workloads** 設定為 1 只會影響新的計畫。已經存在計畫快取中的計畫則不會受到影響。
> 若要立即影響已快取的查詢計畫，需要使用 [ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 清除計畫快取，或必須重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

## <a name="see-also"></a>另請參閱  
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
