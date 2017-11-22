---
title: "變更資料庫相容性模式並使用查詢存放區 | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: "19"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: a230544eba53d9b506aae4bce6feb019820550e6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="change-the-database-compatibility-mode-and-use-the-query-store"></a>變更資料庫相容性模式並使用查詢存放區
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在 SQL Server 2016 和 SQL Server 2017 中，某些變更只有在變更資料庫的 DATABASE_COMPATIBILITY 層級之後才會啟用。 有數種原因可以完成這項作業：  
  
- 因為升級是單向作業 (不可能降級檔案格式)，所以可以將啟用新功能區隔到資料庫內的個別作業。  可以將設定還原為先前的 DATABASE_COMPATIBILITY 層級。  新的模型可減少必須在中斷期間發生的事項數目。  
  
- 查詢處理器的變更會有複雜的影響。  即使系統的「良好」變更對大多數客戶可能不錯，但是可能會造成其他客戶之重要查詢的無法接受衰退。  區隔此邏輯與升級程序，可讓功能 (例如查詢存放區) 快速地降低計畫選擇衰退，或甚至在實際執行伺服器中完全予以避免。  
  
> [!NOTE]  
>  如果使用者資料庫的相容性層級在升級前為 100 或更高層級，則在升級後仍會保持相同。 如果升級前的相容性層級為 90，則在升級後的資料庫中，相容性層級會設定為 100 (這是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]所支援的最低相容性層級)。 tempdb、model、msdb 和 Resource 資料庫的相容性層級在升級之後會設定為目前相容性層級。 master 系統資料庫會繼續保有升級前的相容性層級。 
  
 啟用新查詢處理器功能的升級程序與產品的發行後服務模型有關。  其中某些修正程式是在追蹤旗標 4199 下發行。  需要修正程式的客戶可以選擇這些修正程式，而不會造成其他客戶的非預期衰退。  查詢處理器 Hotfix 的發行後服務模型記載在 [這裡](https://support.microsoft.com/en-us/kb/974006)。 從 SQL Server 2016 開始，移到新的相容性層級表示不再需要 4199 追蹤旗標，因為現在預設會在最新相容性層級中啟用那些修正程式。  因此，在升級程序期間，一定要確認在升級程序完成之後未啟用 4199。  
  
 將查詢處理器升級至最新版本的程式碼的建議工作流程是︰  
  
1.  將資料庫升級至 SQL Server 2016，而不會變更資料庫相容性層級 (將它保留在先前的層級)  
  
2.  在資料庫上啟用查詢存放區。 如需啟用和使用查詢存放區的詳細資訊，請參閱 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)。  
  
3.  請等待足夠的時間來收集工作負載的代表性資料。  
  
4.  將資料庫的相容性層級變更為目前相容性層級。 

   >[!NOTE]
   >最新相容性層級取決於 SQL Server 版本。
   >- SQL Server 2016：130
   >- SQL Server 2017：140

5. 使用 SQL Server Management Studio，評估特定查詢的效能在相容性層級變更之後是否衰退。
  
6.  如果衰退，請強制執行查詢存放區中的先前計畫。  
  
7.  如果無法強制執行查詢計畫，或效能仍然不足，請考慮將相容性層級還原為先前的設定，然後參與 Microsoft 客戶支援。  
  
## <a name="see-also"></a>另請參閱  
 [檢視或變更資料庫的相容性層級](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)  
  
  
