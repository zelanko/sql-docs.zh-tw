---
title: 將整個企業的管理自動化 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fbd32c13badb86db8dae7156b14ca3f93f97d76c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710646"
---
# <a name="automated-administration-across-an-enterprise"></a>將整個企業的管理自動化
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

將多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間的管理自動化，稱為「多伺服器管理」(Multiserver Administration)。 使用多伺服器管理，可進行以下工作：  
  
-   管理二或多部伺服器。  
  
-   為企業伺服器之間的資訊流程進行排程以作為資料倉儲之用。  
  
若要利用多伺服器管理，您至少要有一部主要伺服器與一部目標伺服器。 主要伺服器會將作業散發到目標伺服器，並接收目標伺服器傳回的事件。 對於目標伺服器上執行的作業，主要伺服器也會儲存其作業定義的集中副本。 目標伺服器則會定期連接到主要伺服器，以更新其作業排程。 如果主要伺服器上有新的作業，目標伺服器便會下載該作業。 當目標伺服器完成作業後，它就會重新連接到主要伺服器並報告作業的狀態。 請注意，執行任何資料庫相關活動時，作業定義必須相同。  
  
下圖顯示主要伺服器和目標伺服器之間的關係：  
  
![多伺服器管理組態](../../ssms/agent/media/multisvr.gif "多伺服器管理組態")  
  
如果您負責管理大型公司的部門伺服器，您可以定義下列項目：  
  
-   含多個作業步驟的備份作業。  
  
-   發生備份失敗狀況時要通知的操作員。  
  
-   備份作業的執行排程。  
  
請在主要伺服器上撰寫一次這個備份作業，然後將每個部門伺服器都編列為目標伺服器。 一旦您將這些伺服器編列上去以後，所有的部門伺服器都會執行同一個備份作業，而您只需定義一次作業。  
  
> [!NOTE]  
> 多伺服器管理功能是提供給 sysadmin 角色的成員。 但是，目標伺服器上的 sysadmin 角色成員，不能編輯主要伺服器在目標伺服器上所執行的作業。 這個安全性措施避免意外刪除作業步驟，防止目標伺服器上的作業中斷。  
  
## <a name="in-this-section"></a>本節內容  
[建立多伺服器環境](../../ssms/agent/create-a-multiserver-environment.md)  
包含如何建立與管理主要伺服器及目標伺服器的相關資訊。  
  
[為多伺服器環境選擇適當的 SQL Server Agent 服務帳戶](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
包含針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務使用非管理的 Windows 帳戶或「本機系統」帳戶，會如何影響多伺服器環境的資訊。  
  
[在目標伺服器上設定加密選項](../../ssms/agent/set-encryption-options-on-target-servers.md)  
包含在目標伺服器上設定 MsxEncryptChannelOptions[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 登錄子機碼的相關資訊。  
  
[管理整個企業的作業](../../ssms/agent/manage-jobs-across-an-enterprise.md)  
包含檢查作業狀態、變更作業的目標伺服器、同步處理目標伺服器時鐘，以及向主要伺服器輪詢其目前作業狀態等的相關資訊。  
  
[疑難排解使用 Proxy 的多伺服器作業](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
包含失敗的使用 Proxy 之多伺服器作業的疑難排解資訊。  
  
[輪詢伺服器](../../ssms/agent/poll-servers.md)  
包含如何以隱含方式 (及明確方式) 讓目標伺服器輪詢主要伺服器，以同步處理作業資訊的相關資訊。  
  
[管理事件](../../ssms/agent/manage-events.md)  
包含如何將事件從目標伺服器轉送至主要伺服器的相關資訊。  
  
[微調企業整體的自動化管理](../../ssms/agent/tune-automated-administration-across-an-enterprise.md)  
包含多伺服器環境中的自動化管理如何利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之自行微調功能的相關資訊。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SQL Server Database Engine 的回溯相容性主題](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
[註冊伺服器](../register-servers/register-servers.md)  
[sp_add_targetservergroup](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)  
[sp_delete_targetserver](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)  
[sp_delete_targetservergroup](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)  
[sp_help_downloadlist](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)  
[sp_help_jobserver](../../relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql.md)  
[sp_help_targetservergroup](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)  
[sp_resync_targetserver](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)  
[sp_update_targetservergroup](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)  
[sysjobservers](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)  
[syslogins](../../relational-databases/system-compatibility-views/sys-syslogins-transact-sql.md)  
[systargetservers](../../relational-databases/system-tables/dbo-systargetservers-transact-sql.md)  
  
