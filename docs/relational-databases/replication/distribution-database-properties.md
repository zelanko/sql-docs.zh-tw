---
title: "散發資料庫屬性 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.configdistwizard.distdbproperties.f1
helpviewer_keywords: Distribution Database Properties dialog box
ms.assetid: 0f404ab9-1237-4936-8df5-888baab6a245
caps.latest.revision: "23"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c33a5730c910c0225a11a24b49313bc57d64e29
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="distribution-database-properties"></a>散發資料庫屬性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [散發資料庫屬性] 對話方塊可讓您檢視許多屬性，並設定資料庫的交易保留期限和記錄保留期限。  
  
## <a name="options"></a>選項。  
 **名稱**  
 散發資料庫的名稱，預設為「distribution」(唯讀)。  
  
 **檔案位置**  
 資料庫檔案和記錄檔的位置 (唯讀)。  
  
 **交易保留期限**  
 又稱為散發保留期限。 交易的儲存時間長度，適用於異動複寫。 如需詳細資訊，請參閱 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 **記錄保留期限**  
 記錄中繼資料的儲存時間長度，適用於所有類型的複寫。  
  
 **佇列讀取器代理程式安全性**  
 佇列讀取器代理程式會用於具有佇列更新訂閱的異動複寫。 如果您在新增發行集精靈的 **[發行集類型]** 頁面上選取 **[具更新訂閱的交易式發行集]** ，則會自動建立佇列讀取器代理程式。 按一下 **[安全性設定]** ，即可變更執行代理程式和連接散發者的帳戶。  
  
 在此頁面上選取 **[建立佇列讀取器代理程式]** 也可以建立佇列讀取器代理程式 (如果已建立代理程式，此選項會停用)。  
  
 有兩個地方可以指定佇列讀取器代理程式的其他連接資訊：  
  
-   代理程式會使用 **[發行者屬性]** 對話方塊中指定的認證來連接發行者，該對話方塊可以從 **[散發者屬性]** 對話方塊的 **[發行者]** 頁面存取。  
  
-   代理程式會使用新增訂閱精靈中為散發代理程式指定的認證，來連接訂閱者。  
  
 如需詳細資訊，請參閱  [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## <a name="see-also"></a>另請參閱  
 [[設定散發]](../../relational-databases/replication/configure-distribution.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  
