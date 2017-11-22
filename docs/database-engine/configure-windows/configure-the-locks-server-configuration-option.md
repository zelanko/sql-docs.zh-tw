---
title: "設定 locks 伺服器組態選項 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: locks option [SQL Server]
ms.assetid: b0cf0f86-7652-4574-a9fb-908e10d03973
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 618bcb7cb309f80036cae13f55191f3d34ae6b4c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="configure-the-locks-server-configuration-option"></a>設定 locks 伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] locks [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **locks** 選項會設定可用鎖定的最大數目，藉此限制 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 用於鎖定的記憶體數量。 預設值為 0，允許 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 根據變更系統需求，動態配置與取消配置鎖定結構。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 locks 選項：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **待處理**  [設定 locks 選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   如果伺服器啟動時是將 **locks** 設為 0，則鎖定管理員會從 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 取得足夠的記憶體，以供 2,500 個鎖定結構的初始集區使用。 當鎖定集區耗盡時，就會再為集區取得額外的記憶體。  
  
     一般而言，如果鎖定集區所需的記憶體多於 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 記憶體集區可提供的數量，而且還有更多的電腦記憶體可用 (尚未達到 **max server memory** 臨界值) 的話， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會動態配置記憶體，以滿足鎖定要求。 然而，如果配置該記憶體會造成作業系統層級的分頁 (例如，如果另一個應用程式與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體在同一部電腦上執行而且它正在使用該記憶體)，就無法再配置鎖定空間。 動態鎖定集區所取得的記憶體不會超過 [!INCLUDE[ssDE](../../includes/ssde-md.md)]配置記憶體的 60%。 當鎖定集區達到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體所取得之記憶體的 60%，或電腦上沒有多餘的記憶體可用時，之後的鎖定要求都會產生錯誤。  
  
     讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 動態地使用鎖定，是建議的設定。 但是，您可以設定 **locks** ，並覆寫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 動態配置鎖定資源的功能。 當 **locks** 設為 0 以外的數值時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所能配置的鎖定無法超過 **locks**中指定的值。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 顯示訊息表示已超過可用的鎖定個數，就應增加這個值。 因為每個鎖定都會耗用記憶體 (每個鎖定 96 個位元組)，所以增加這個值可能需要增加伺服器專用的記憶體數量。  
  
-   **locks** 選項也會影響發生鎖定擴大的時機。 **locks** 設為 0 時，鎖定擴大會在目前的鎖定結構所用的記憶體達到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 記憶體集區的 40% 時發生。 **locks** 未設為 0 時，鎖定擴大會在鎖定個數達到 **locks**指定數值的 40% 時發生。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-locks-option"></a>若要設定 locks 選項  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[進階]** 節點。  
  
3.  在 **[平行處理原則]**下，輸入所需的 **locks** 選項值。  
  
     使用 **locks** 選項來設定可用鎖定的最大數目，從而限制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用於鎖定的記憶體數量。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-locks-option"></a>若要設定 locks 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例示範如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 設定 `locks` 選項的值，將可供所有使用者使用的鎖定數目設定為 `20000`。  
  
```tsql  
Use AdventureWorks2012 ;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'locks', 20000;  
GO  
RECONFIGURE;  
GO  
```  
  
 如需詳細資訊，請參閱 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="FollowUp"></a> 待處理：設定 locks 選項之後  
 伺服器必須重新啟動之後，設定才能生效。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
