---
title: "將整個企業的管理自動化 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 618e199812a39ec29e032f8371419ec6184c713f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="automated-administration-across-an-enterprise"></a>將整個企業的管理自動化
將多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行個體之間的管理自動化，稱為「多伺服器管理」(Multiserver Administration)。 使用多伺服器管理，可進行以下工作：  
  
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
包含針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務使用非管理的 Windows 帳戶或「本機系統」帳戶，會如何影響多伺服器環境的資訊。  
  
[在目標伺服器上設定加密選項](../../ssms/agent/set-encryption-options-on-target-servers.md)  
包含在目標伺服器上設定 MsxEncryptChannelOptions[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 登錄子機碼的相關資訊。  
  
[管理整個企業的作業](../../ssms/agent/manage-jobs-across-an-enterprise.md)  
包含檢查作業狀態、變更作業的目標伺服器、同步處理目標伺服器時鐘，以及向主要伺服器輪詢其目前作業狀態等的相關資訊。  
  
[疑難排解使用 Proxy 的多伺服器作業](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
包含失敗的使用 Proxy 之多伺服器作業的疑難排解資訊。  
  
[輪詢伺服器](../../ssms/agent/poll-servers.md)  
包含如何以隱含方式 (及明確方式) 讓目標伺服器輪詢主要伺服器，以同步處理作業資訊的相關資訊。  
  
[管理事件](../../ssms/agent/manage-events.md)  
包含如何將事件從目標伺服器轉送至主要伺服器的相關資訊。  
  
[微調企業整體的自動化管理](../../ssms/agent/tune-automated-administration-across-an-enterprise.md)  
包含多伺服器環境中的自動化管理如何利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]之自行微調功能的相關資訊。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SQL Server Database Engine 的回溯相容性主題](http://msdn.microsoft.com/en-us/10de5ec6-d3cf-42ef-aa62-1bdf3fbde841)  
[註冊伺服器](http://msdn.microsoft.com/en-us/c2a2513e-fa09-419c-99e7-a12d57c5a0db)  
[sp_add_targetservergroup](http://msdn.microsoft.com/en-us/acb69343-d766-46ff-b771-0c7655c5231a)  
[sp_delete_targetserver](http://msdn.microsoft.com/en-us/cc438701-ad91-419d-9f23-ebc4c548c700)  
[sp_delete_targetservergroup](http://msdn.microsoft.com/en-us/d8dd838e-64aa-419f-9ccb-ff04908cf3e4)  
[sp_help_downloadlist](http://msdn.microsoft.com/en-us/745b265b-86e8-4399-b928-c6969ca1a2c8)  
[sp_help_jobserver](http://msdn.microsoft.com/en-us/57971787-f9f5-4199-9f64-c2b61a308906)  
[sp_help_targetservergroup](http://msdn.microsoft.com/en-us/ec3a4a68-b591-431c-9518-053ede522d0c)  
[sp_resync_targetserver](http://msdn.microsoft.com/en-us/40e44df7-d3e3-44ee-b149-08aba629a21f)  
[sp_update_targetservergroup](http://msdn.microsoft.com/en-us/4ac65ed6-e07e-40e4-a282-13bfd92dfa41)  
[sysjobservers](http://msdn.microsoft.com/en-us/9abcc20f-a421-4591-affb-62674d04575e)  
[syslogins](http://msdn.microsoft.com/en-us/4cb34f17-a4bb-469f-a218-71f074e6308f)  
[systargetservers](http://msdn.microsoft.com/en-us/479d1314-be37-4d19-ac9c-419fc9110e53)  
  

