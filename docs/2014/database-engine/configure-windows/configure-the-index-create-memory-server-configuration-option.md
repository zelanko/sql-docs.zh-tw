---
title: 設定 index create memory 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- index create memory option
ms.assetid: 3d722d9b-bada-4bf5-a9d7-bfc556bb4915
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6cd0aeb93d3fb68089338335068fdaaae19919fa
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935686"
---
# <a name="configure-the-index-create-memory-server-configuration-option"></a>設定 index create memory 伺服器組態選項
  此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] index create memory [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **index create memory** 選項會控制最初配置來建立索引的記憶體數量上限。 這個選項的預設值是 0 (自我設定)。 若稍後在建立索引時需要更多記憶體，且有足夠的記憶體可用，則伺服器會使用該記憶體，因而超過此選項的設定。 若沒有更多可用的記憶體，則會使用預先配置的記憶體繼續進行索引建立作業。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 index create memory 選項：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：** [設定索引建立記憶體選項之後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   **[每個查詢的最小記憶體]** 選項之設定，優先順序高於 **[索引建立記憶體]** 選項。 若您同時變更了兩個選項，且 **index create memory** 小於 **min memory per query**，您會看到警告訊息，但仍會設定該值。 執行查詢時，您會看到同樣的警告。  
  
-   使用資料分割資料表與索引時，如果有非對齊之資料分割索引與高度平行處理，建立索引時所需的最低記憶體需求會大幅增加。 此選項會控制在單一索引建立作業中，為所有索引資料分割配置的初始記憶體數量總計。 若此選項設定的記憶體數量小於執行查詢所需的最低記憶體需求，則查詢會終止，且會顯示錯誤訊息。  
  
-   此選項的執行值將不會超過執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之作業系統與硬體平台可用的實際記憶體數量。 在 32 位元作業系統上，執行值會低於 3 GB。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   **[索引建立記憶體]** 選項為自我設定，並且通常不需要調整便可使用。 然而，如果無法建立索引，請考慮增加這個選項的執行值。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-index-create-memory-option"></a>若要設定 index create memory 選項  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]  。  
  
2.  按一下 **[記憶體]** 節點。  
  
3.  在 **[索引建立記憶體]** 之下，輸入或選取所要的索引建立記憶體選項值。  
  
     **index create memory** 選項可用來控制索引建立排序所使用的記憶體大小。 [索引建立記憶體]**** 屬於自我設定的選項，而且不需調整即可適用於大部份情況。 然而，如果無法建立索引，請考慮增加這個選項的執行值。 查詢排序是透過 **min memory per query** 選項來控制。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-index-create-memory-option"></a>若要設定 index create memory 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 將 `index create memory` 選項的值設定為 `4096`。  
  
```sql  
USE AdventureWorks2012 ;  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
EXEC sp_configure 'index create memory', 4096  
GO  
RECONFIGURE;  
GO  
```  
  
 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="follow-up-after-you-configure-the-index-create-memory-option"></a><a name="FollowUp"></a> 待處理：設定 index create memory 選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [sys.configurations &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-configurations-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器記憶體伺服器設定選項](server-memory-server-configuration-options.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
