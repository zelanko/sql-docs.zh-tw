---
title: 變更資料庫相容性層級並使用查詢存放區 | Microsoft Docs
ms.custom: ''
ms.date: 07/21/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f1a7ba5b39513cd39226e8b671a6634c547d95c9
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="change-the-database-compatibility-level-and-use-the-query-store"></a>變更資料庫相容性層級並使用查詢存放區

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，某些變更只在[資料庫相容性層級](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)變更後才啟用。 有數種原因可以完成這項作業：  
  
- 因為升級是單向作業 (不可能降級檔案格式)，所以可以將啟用新功能區隔到資料庫內的個別作業。 設定可還原為先前的資料庫相容性層級。  新的模型可減少必須在中斷期間發生的事項數目。  
  
- 查詢處理器的變更會有複雜的影響。 即使對系統進行「良好」變更對多數工作負載而言可能有益，但可能造成其他工作負載的重要查詢發生無法接受的迴歸。 將此邏輯與升級程序區隔可讓功能 (例如查詢存放區) 快速降低計畫選擇迴歸，或甚至在生產伺服器中予以完全避免。  
  
> [!IMPORTANT]  
> 附加或還原資料庫以及就地升級之後，[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 預期會有下列行為：
> - 如果使用者資料庫的相容性層級在升級前為 100 或更高層級，則在升級後仍會保持相同。    
> - 如果使用者資料庫在升級前的相容性層級為 90，則在升級後的資料庫中，相容性層級會設定為 100，這是 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 支援的最低相容性層級)。    
> - tempdb、model、msdb 和 Resource 資料庫的相容性層級在升級之後會設定為目前相容性層級。   
> - master 系統資料庫會繼續保有升級前的相容性層級。    
  
啟用新查詢處理器功能的升級程序與產品的發行後服務模型有關。  其中某些修正是在[追蹤旗標 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199) 下所發行。  需要修正程式的客戶可以選擇這些修正程式，而不會造成其他客戶的非預期衰退。 查詢處理器 Hotfix 的發行後服務模型記載在 [這裡](http://support.microsoft.com/kb/974006)。 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 開始，移到新的相容性層級表示不再需要追蹤旗標 4199，原因是現在預設會在最新的相容性層級中啟用那些修正。 因此，在升級程序期間，一定要確認在升級程序完成之後未啟用 4199。  

> [!NOTE]
> 不過，如果適用的話，仍需追蹤旗標 4199，以啟用在 RTM 後發行的任何新查詢處理器修正。
  
如需將查詢處理器程式碼升級至最新版，建議遵循以下工作流程，其說明請參閱[查詢存放區使用案例的在升級至較新 SQL Server 期間保持效能穩定性一節](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade)。  
  
![query-store-usage-5](../../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5") 
 
## <a name="see-also"></a>另請參閱  
[檢視或變更資料庫的相容性層級](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)     
[查詢存放區使用案例](../../relational-databases/performance/query-store-usage-scenarios.md)     
[ALTER DATABASE &#40;Transact-SQL&#41; 相容性層級](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)
    
  
