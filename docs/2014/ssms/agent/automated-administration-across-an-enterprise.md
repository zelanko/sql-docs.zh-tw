---
title: 將整個企業的管理自動化 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enterprise automatic administration [SQL Server]
- multiserver administration [SQL Server]
- SQL Server Agent jobs, multiserver administration
- jobs [SQL Server Agent], multiserver administration
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- master servers [SQL Server]
- multiple instances of SQL Server
- target servers [SQL Server]
ms.assetid: 44d8365b-42bd-4955-b5b2-74a8a9f4a75f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8df3e34c2c70c81f9710ade0d6855446b930fb50
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011801"
---
# <a name="automated-administration-across-an-enterprise"></a>將整個企業的管理自動化
  將多個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之間的管理自動化，稱為「多伺服器管理」**(Multiserver Administration)。 使用多伺服器管理，可進行以下工作：  
  
-   管理二或多部伺服器。  
  
-   為企業伺服器之間的資訊流程進行排程以作為資料倉儲之用。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 持續努力減少整體擁有成本的過程中，[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 導入了兩項功能：稱為「原則式管理」的管理伺服器方法，以及使用組態伺服器和伺服器群組的多伺服器查詢。 這些功能可以搭配本主題所描述的某些功能使用，也可以取代這些功能。 如需詳細資訊，請參閱[使用以原則為基礎的管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)和[使用中央管理伺服器管理多部伺服器](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)。  
  
 若要利用多伺服器管理，您至少要有一部主要伺服器與一部目標伺服器。 主要伺服器會將作業散發到目標伺服器，並接收目標伺服器傳回的事件。 對於目標伺服器上執行的作業，主要伺服器也會儲存其作業定義的集中副本。 目標伺服器則會定期連接到主要伺服器，以更新其作業排程。 如果主要伺服器上有新的作業，目標伺服器便會下載該作業。 當目標伺服器完成作業後，它就會重新連接到主要伺服器並報告作業的狀態。  
  
 下圖顯示主要伺服器和目標伺服器之間的關係：  
  
 ![多伺服器管理組態](../../database-engine/media/multisvr.gif "多伺服器管理組態")  
  
 如果您負責管理大型公司的部門伺服器，您可以定義下列項目：  
  
-   含多個作業步驟的備份作業。  
  
-   發生備份失敗狀況時要通知的操作員。  
  
-   備份作業的執行排程。  
  
 請在主要伺服器上撰寫一次這個備份作業，然後將每個部門伺服器都編列為目標伺服器。 一旦您將這些伺服器編列上去以後，所有的部門伺服器都會執行同一個備份作業，而您只需定義一次作業。  
  
> [!NOTE]  
>  多伺服器管理功能是提供給 sysadmin 角色的成員。 但是，目標伺服器上的 sysadmin 角色成員，不能編輯主要伺服器在目標伺服器上所執行的作業。 這個安全性措施避免意外刪除作業步驟，防止目標伺服器上的作業中斷。  
  
## <a name="in-this-section"></a>本節內容  
 [建立多伺服器環境](create-a-multiserver-environment.md)  
 包含如何建立與管理主要伺服器及目標伺服器的相關資訊。  
  
 [為多伺服器環境選擇適當的 SQL Server Agent 服務帳戶](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
 包含針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 服務使用非管理的 Windows 帳戶或「本機系統」帳戶，會如何影響多伺服器環境的資訊。  
  
 [在目標伺服器上設定加密選項](set-encryption-options-on-target-servers.md)  
 包含在目標伺服器上設定 MsxEncryptChannelOptions [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 登錄子機碼的相關資訊。  
  
 [管理整個企業的作業](manage-jobs-across-an-enterprise.md)  
 包含檢查作業狀態、變更作業的目標伺服器、同步處理目標伺服器時鐘，以及向主要伺服器輪詢其目前作業狀態等的相關資訊。  
  
 [為使用 Proxy 的多伺服器作業疑難排解](troubleshoot-multiserver-jobs-that-use-proxies.md)  
 包含失敗的使用 Proxy 之多伺服器作業的疑難排解資訊。  
  
 [輪詢伺服器](poll-servers.md)  
 包含如何以隱含方式 (及明確方式) 讓目標伺服器輪詢主要伺服器，以同步處理作業資訊的相關資訊。  
  
 [管理事件](manage-events.md)  
 包含如何將事件從目標伺服器轉送至主要伺服器的相關資訊。  
  
 [微調企業整體的自動化管理](tune-automated-administration-across-an-enterprise.md)  
 包含多伺服器環境中的自動化管理如何利用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]之自行微調功能的相關資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Database Engine 回溯相容性](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [註冊伺服器](../register-servers/register-servers.md)   
 [sp_add_targetservergroup &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql)   
 [sp_delete_targetserver &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql)   
 [sp_delete_targetservergroup &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql)   
 [sp_help_downloadlist &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql)   
 [sp_help_jobserver &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql)   
 [sp_help_targetservergroup &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql)   
 [sp_resync_targetserver &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)   
 [sp_update_targetservergroup &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql)   
 [dbo.sysjobservers &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysjobservers-transact-sql)   
 [sys.sys登入 &#40;Transact-sql&#41;](/sql/relational-databases/system-compatibility-views/sys-syslogins-transact-sql)   
 [dbo.systargetservers &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-systargetservers-transact-sql)  
  
  
