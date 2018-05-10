---
title: 檢視或設定 backup compression default 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], backup compression default option
- backup compression [SQL Server], backup compression default Option
ms.assetid: 23029395-3e93-4c29-b7d6-e5a47a3526ff
caps.latest.revision: 30
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ae83b4a7df944cc0e2b7576a2297e120bd2305a3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="view-or-configure-the-backup-compression-default-server-configuration-option"></a>檢視或設定 backup compression default 伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中檢視或設定 [備份壓縮預設] 伺服器組態選項。 **backup compression default** 選項決定伺服器執行個體根據預設是否會建立壓縮備份。 安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時， **ssCurrent** 選項已關閉。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **使用下列方法檢視或設定 backup compression default 選項：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **待處理**  [設定 backup compression default 選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   並非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有版本中都提供備份壓縮。 如需詳細資訊，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
-   根據預設，壓縮會大幅增加 CPU 使用量，而且壓縮程序所耗用的額外 CPU 可能會對並行作業造成不良的影響。 因此，您可能會想要在[資源管理員](../../relational-databases/resource-governor/resource-governor.md)限制 CPU 使用量的工作階段中建立低優先權的壓縮備份。 如需詳細資訊，請參閱本主題稍後介紹的＜ [使用資源管理員進行備份壓縮，以限制 CPU 使用率 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)限制的工作階段中，建立低優先權的壓縮備份。  
  
###  <a name="Recommendations"></a> 建議  
  
-   當您建立個別備份、設定記錄傳送組態或建立維護計畫時，可以覆寫伺服器層級的預設值。  
  
-   備份壓縮同時支援磁碟備份裝置和磁帶備份裝置。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-configure-the-backup-compression-default-option"></a>檢視或設定 backup compression default 選項  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[資料庫設定]** 節點。  
  
3.  在 **[備份與還原]** 底下， **[壓縮備份]** 會顯示 **backup compression default** 選項的目前設定。 這項設定會決定壓縮備份的伺服器層級預設值，如下所示：  
  
    -   如果 **[壓縮備份]** 方塊是空的，新備份預設不會進行壓縮。  
  
    -   如果 **[壓縮備份]** 方塊已核取，新備份預設就會進行壓縮。  
  
     如果您是 **sysadmin** 或 **serveradmin** 固定伺服器角色的成員，也可以透過按一下 **[壓縮備份]** 方塊，變更預設值。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-backup-compression-default-option"></a>檢視 backup compression default 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例會查詢 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 目錄檢視以判斷 `backup compression default`的值。 值為 0 表示備份壓縮已關閉，值為 1 表示備份壓縮已啟用。  
  
```sql  
SELECT value   
FROM sys.configurations   
WHERE name = 'backup compression default' ;  
GO  
```  
  
#### <a name="to-configure-the-backup-compression-default-option"></a>設定 backup compression default 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例示範如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) ，將伺服器執行個體設定為依預設會建立壓縮備份。  
  
```sql  
EXEC sp_configure 'backup compression default', 1 ;  
RECONFIGURE WITH OVERRIDE ;  
GO 
```  
  
 如需詳細資訊，請參閱 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)的所有版本中都提供備份壓縮。  
  
##  <a name="FollowUp"></a> 待處理：設定 backup compression default 選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
  
  

