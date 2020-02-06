---
title: 設定 user connections 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- simultaneous connections [SQL Server]
- user connections option [SQL Server]
- users [SQL Server], simultaneous connections
- maximum number of simultaneous user connections
- connections [SQL Server], simultaneous
ms.assetid: 53beee6e-59fe-4276-9abb-8f1cec2a3508
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 09062541d167be92c40877033e46eec6ebd1c98f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68012176"
---
# <a name="configure-the-user-connections-server-configuration-option"></a>設定 user connections 伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] user connections [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **user connections** 選項會指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上可同時連接的使用者數目上限。 實際允許的使用者連接數也取決於您所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本，以及應用程式的限制或應用程式和硬體的限制而定。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最多允許 32,767 個使用者連接。 因為 **user connections** 是動態的 (自我設定的) 選項，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會視需要自動調整最大使用者連接數，最多調整到允許的最大值。 例如，如果只有 10 個使用者登入，就配置 10 個使用者連線物件。 在大部分情況下，不需要變更這個選項的值。 預設值為 0，表示允許最大量 (32,767) 的使用者連接數。  
  
 若要判斷系統允許的最大使用者連接數目，您可以執行 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 或查詢 [sys.configuration](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 目錄檢視。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 user connections 選項：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：** [設定使用者連線選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   此選項是進階選項，只有具經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專業人員才可變更。  
  
-   使用 **user connections** 選項有助於避免因並行連接過多，而導致伺服器超過負載。 您可以根據系統與使用者需求估計連接數。 例如，在有許多使用者的系統上，通常不會每個使用者各要求一個唯一的連接。 連接可以由使用者共用。 執行 OLE DB 應用程式的使用者，對每個開啟的連接物件都必須各有一個連接；執行開放式資料庫連接 (ODBC) 應用程式的使用者，對應用程式中的每個使用中連接控制代碼都必須各有一個連接；而執行 DB-Library 應用程式的使用者，則對呼叫 DB-Library **dbopen** 函數的每個啟動處理序都必須各有一個連接。  
  
    > [!IMPORTANT]  
    >  如果必須使用這個選項，請不要將這個值設得太大，因為每個連接不論使用與否，都會造成額外負擔。 如果超過最大使用者連接數，就會收到錯誤訊息，然後要等到可以使用另一個連接後，才能再繼續進行連接。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-user-connections-option"></a>設定 user connections 選項  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下伺服器，然後按一下 **[屬性]** 。  
  
2.  按一下 **[連接]** 節點。  
  
3.  在 **[連接]** 下的 **[並行連接的最大數目]** 方塊中，輸入或選取 0 至 32767 之間的值，以設定可同時連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的最大使用者數目。  
  
4.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-user-connections-option"></a>設定 user connections 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 以將 `user connections` 選項的值設定為 `325` 位使用者。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'user connections', 325 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="FollowUp"></a> 後續操作：設定使用者連線選項之後  
 伺服器必須重新啟動之後，設定才能生效。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
