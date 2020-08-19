---
description: 訂閱逾期與停用
title: 訂閱逾期與停用 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distributors [SQL Server replication], distribution retention period
- subscriptions [SQL Server replication], expiration
- publications [SQL Server replication], publication retention periods
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- publication retention periods
- distribution retention period
- subscriptions [SQL Server replication], deactivation
- deactivating subscriptions
ms.assetid: 4d03f5ab-e721-4f56-aebc-60f6a56c1e07
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 64fb9d21457558d2d0f3373b926f426808b9105d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423402"
---
# <a name="subscription-expiration-and-deactivation"></a>訂閱逾期與停用
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  如果訂閱在指定 *「保留期限」* 內未執行同步處理，則可以停用訂閱或使訂閱過期。 發生的動作依複寫類型及超過的保留期限而定。  
  
 若要設定保留期限，請參閱[設定訂閱的逾期期限](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)、[設定交易式發行集的散發保留期限 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/set-distribution-retention-period-for-transactional-publications.md) 和[設定發行與散發](../../relational-databases/replication/configure-publishing-and-distribution.md)。  
  
## <a name="transactional-replication"></a>異動複寫  
 異動複寫使用最長散發保留期限 ([sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) 的 `@max_distretention` 參數) 和發行集保留期限 ([sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 的 `@retention` 參數)：  
  
-   如果在最高散發保留期限內 (預設值為 72 小時) 未同步處理訂閱，並且散發資料庫中有變更尚未傳遞至「訂閱者」，則「散發者」上執行的 **Distribution clean up** 工作會將訂閱標記為停用。 訂閱必須重新初始化。  
  
-   如果在發行集保留期限內 (預設值為 336 小時) 未同步處理訂閱，則訂閱將過期並由「發行者」上執行的 **Expired subscription clean up** 工作卸除。 訂閱必須重新建立並同步處理。  
  
     若發送訂閱已過期，會完全移除；但提取訂閱不會移除。 您必須在訂閱者端清除提取訂閱。 如需詳細資訊，請參閱 [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)。  
  
## <a name="merge-replication"></a>合併式複寫  
 合併式複寫使用發行集保留期限 ([sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 的 `@retention` 和 `@retention_period_unit` 參數)。 訂閱過期後，就必須重新初始化，因為訂閱的中繼資料已被移除。 未重新初始化的訂閱，由「發行者」上執行的 **Expired subscription clean up** 作業卸除。 依預設此作業每日執行，並移除所有尚未同步處理為兩倍發行保留期限的發送訂閱。 例如：  
  
-   若發行的保留期限為 14 天，訂閱若未於 14 天內同步處理就會過期。  
  
     如果發行者正在執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本，且訂閱的代理程式來自 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本，則訂閱只有在該訂閱分割資料變更時才會過期。 例如，假設訂閱者收到德國客戶的客戶資料。 若保留期限設定為 14 天，只有當德國客戶資料在過去 14 天變更，訂閱才會在第14 天過期。  
  
-   從上一次同步處理後的第 14 到 27 天，訂閱皆可重新初始化。  
  
-   在上一次同步處理後的 28 天，訂閱由 **Expired subscription clean up** 作業卸除。 若發送訂閱已過期，會完全移除；但提取訂閱不會移除。 您必須在訂閱者端清除提取訂閱。 如需詳細資訊，請參閱 [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)。  
  
### <a name="considerations-for-setting-the-publication-retention-period-for-merge-publications"></a>設定合併式發行集保留期限的考量  
 設定合併式發行集的保留期限時，請記住以下考量：  
  
-   合併式發行集的保留期限具有 24 小時寬限期，可配合不同時區的「訂閱者」。 例如，如果您設定的保留期限是一天，實際的保留期限便是 48 小時。  
  
-   合併式複寫中繼資料的清除相依於發行集保留期限：  
  
    -   複寫無法在發行集和訂閱資料庫中清除中繼資料，直到到達保留期限為止。 小心指定保留期限的高數值，因為此值可能對複寫效能產生負面影響。 若您能夠確實預測所有訂閱者都會在該時間週期內定期同步處理，建議您使用較低設定。  
  
    -   可以指定訂閱永不過期 ( `@retention` 的值為 0)，但強烈建議您不要使用此值，因為中繼資料無法清除。  
  
-   任何重新發行者的保留期限必須設定為等於或少於原始「發行者」的設定值。 對所有的「發行者」及其替代性同步處理夥伴，也應該使用相同的發行保留值。 使用不同值可能會導致非交集的情況。 若您需要變更發行集保留值，請重新初始化訂閱者，以避免資料無法聚合。  
  
-   在清除之後，如果發行集保留期限加長，而訂閱嘗試與發行者 (已刪除中繼資料) 合併，則由於保留值增加而使訂閱不會過期。 不過，發行者則會因沒有足夠的中繼資料可以下載訂閱者的變更，而導致無法聚合。  
  
## <a name="see-also"></a>另請參閱  
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [複寫代理程式管理](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
