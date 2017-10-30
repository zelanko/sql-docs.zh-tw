---
title: "逐步解說： 設定 SQL Server Integration Services 向外的延展 |Microsoft 文件"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 685286966599c4dcd3dc2f7029413c77f3ff2689
ms.openlocfilehash: c386b01043764405872365af379cfdedb036b65f
ms.contentlocale: zh-tw
ms.lasthandoff: 10/20/2017

---
# <a name="walkthrough-set-up-integration-services-scale-out"></a>逐步解說：設定 Integration Services 相應放大
設定[!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)]向外藉由完成下列工作。 

> [!NOTE]
> 如果您要在一部電腦上安裝向外，請同時安裝標尺出主要和標尺出背景工作的功能。 當您同時安裝這些功能時，會自動產生端點，以連接至相應放大主機。 

* [安裝相應放大主機](#InstallMaster)

* [安裝相應放大背景工作](#InstallWorker)

* [安裝相應放大背景工作用戶端憑證](#InstallCert)

* [開啟防火牆通訊埠](#Firewall)

* [啟動 SQL Server 相應放大主機和背景工作服務](#Start)

* [啟用相應放大主機](#EnableMaster)

* [啟用 SQL Server 驗證模式](#EnableAuth)

* [啟用相應放大背景工作](#EnableWorker)

## <a name="InstallMaster"></a> 安裝相應放大主機

若要啟用的標尺出主要功能，您必須安裝 Database Engine Services、 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)]，及其標尺出主要功能，當您設定[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 

如需設定 Database Engine Services 和 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 的相關資訊，請參閱[安裝 SQL Server Database Engine](../../database-engine/install-windows/install-sql-server-database-engine.md) 和[安裝 Integration Services](../install-windows/install-integration-services.md)。
> [!NOTE]
> 若要使用標尺出記錄的預設 SQL 驗證帳戶，[資料庫引擎組態] 頁面上的驗證模式資料庫引擎安裝期間選取混合模式。 請參閱[變更的帳戶向外記錄](change-logdb-account.md)如需詳細資訊。

**若要安裝相應放大主機功能，請使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈或命令提示字元。**

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈的步驟
  1.  在**特徵選取**頁面上，選取**標尺出主要**， 下[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。   
  ![特徵選取主機](media/feature-select-master.PNG)
  
  2.  在 [伺服器組態]  頁面上，選取要執行 [SQL Server Integration Services 相應放大主機服務]  的帳戶，然後選取 [啟動類型] 。  
  ![伺服器組態](media/server-config.PNG)
  3.  在 [Integration Services 相應放大主機組態]  頁面上，指定相應放大主機用來與相應放大背景工作通訊的通訊埠編號。 預設通訊埠編號是 8391。  
  ![主要組態](media/master-config.PNG "主要組態")
  4.  指定用來執行下列其中一項動作來保護標尺出主要和標尺出背景工作之間的通訊的 SSL 憑證。
    * 讓安裝程序，即可建立預設的自我簽署的 SSL 憑證**建立新的 SSL 憑證**。  預設憑證會安裝到 [受信任的根憑證授權單位] 的 [本機電腦] 下方。 您可以指定此憑證的 Cn。 主要端點的主機名稱應該併入 Cn。 根據預設，電腦名稱和 ip 的主要節點會包含。
    * 選取現有的 SSL 憑證在本機電腦上，依序按一下**使用現有的 SSL 憑證**，然後按一下**瀏覽**選取憑證。 憑證的指紋會出現在文字方塊中。 按一下 [瀏覽]  會顯示在 [受信任的根憑證授權單位] 的 [本機電腦] 中所儲存的憑證。 您選取的憑證必須儲存在這裡。       
![主要設定 2](media/master-config-2.PNG "主要設定 2")
  5.  完成 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈。
- 命令提示字元的步驟

    請遵循[從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 中的指示進行。 執行下列動作，以設定相應放大主機相關參數。
  1.  將 IS_Master 新增至 /FEATURES 參數
  2.  藉由指定下列參數和其值設定標尺出主要： /ISMASTERSVCACCOUNT、 /ISMASTERSVCPASSWORD、 /ISMASTERSVCSTARTUPTYPE、 /ISMASTERSVCPORT，/ISMasterSVCSSLCertCN(optional)、 /ISMASTERSVCTHUMBPRINT(optional)。

> [!Note]
> 如果標尺出主要未安裝 Database Engine 一起，而且 Database Engine 的具名執行個體，您需要在安裝後設定 SqlServerName 標尺出主要服務組態檔中。 請參閱[標尺出主要](integration-services-ssis-scale-out-master.md)如需詳細資訊。

## <a name="InstallWorker"></a> 安裝相應放大背景工作
 
若要啟用相應放大背景工作功能，您必須在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝時安裝 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 和其相應放大背景工作功能。

**若要安裝相應放大背景工作功能，請使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈或命令提示字元。**

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈的步驟
  1.  在**特徵選取**頁面上，選取**標尺出工作者**， 下[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。   
  ![特徵選取背景工作](media/feature-select-worker.PNG)
  2. 在 [伺服器組態]  頁面上，選取要執行 [SQL Server Integration Services 相應放大背景工作服務]  的帳戶，然後選取 [啟動類型] 。    
  ![伺服器組態 2](media/server-config-2.PNG "伺服器設定 2")
  3. 在 [Integration Services 相應放大背景工作組態]  頁面上，指定連接至相應放大主機的端點。 
      > [!Note]
      > 您可這裡略過背景工作節點組態 （步驟 3 和 4），並將關聯的標尺出工作者以標尺出母片[標尺出管理員](integration-services-ssis-scale-out-manager.md)安裝之後。

    - 如**一部電腦**環境中，端點會在標尺出主要和標尺出背景工作會同時安裝時自動產生。 
    - 如**多部電腦**環境中，端點所組成的名稱或電腦的 IP 標尺出 Master，安裝與標尺出主要安裝期間指定的連接埠號碼。    
   ![背景工作設定 1](media/worker-config.PNG "背景工作設定 1")    

  4. 如**多部電腦**環境中，指定用來驗證標尺出主要的用戶端 SSL 憑證。 如**一部電腦**環境中，不需要指定用戶端 SSL 憑證。 
  
     > [!NOTE]
     > 標尺出主機所使用的 SSL 憑證是自我簽署，對應的用戶端 SSL 憑證時必須具有標尺出背景工作的電腦上安裝。 如果您提供的檔案路徑用戶端 SSL 憑證上**Integration Services 出工作者調整組態規模** 頁面上，憑證會自動安裝; 否則您必須稍後手動安裝憑證。 
     
     按一下 [瀏覽]  找出憑證檔案 (*.cer)。 若要使用的預設 SSL 憑證，選取 SSISScaleOutMaster.cer 檔案位於\<磁碟機\>: \Program Files\Microsoft SQL Server\140\DTS\Binn 標尺出主要安裝所在的電腦上。   
   ![背景工作設定 2](media/worker-config-2.PNG "背景工作設定 2")
  5. 完成 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈。
- 命令提示字元的步驟

    請遵循[從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 中的指示進行。 執行下列動作，以設定相應放大背景工作相關參數。
    1.  將 IS_Worker 新增至 /FEATURES 參數
    2. 設定標尺出 Worker，指定下列參數和值： /ISWORKERSVCACCOUNT、 /ISWORKERSVCPASSWORD、 /ISWORKERSVCSTARTUPTYPE，/ISWORKERSVCMASTER(optional)、 /ISWORKERSVCCERT(optional)。

 
## <a name="InstallCert"></a> 安裝相應放大背景工作用戶端憑證

在標尺出工作者的安裝時，背景工作憑證會自動建立及安裝在電腦上。 同時，會在 \<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn 下方安裝對應的用戶端憑證 SSISScaleOutWorker.cer。 標尺出主要驗證標尺出背景工作，您必須將此用戶端憑證新增到標尺出主機之本機電腦的根存放區。
  
若要將用戶端憑證新增至根存放區，請連按兩下 .cer 檔案，然後按一下憑證 對話方塊中的 安裝憑證  。 即會顯示 [憑證匯入精靈]  。  

## <a name="Firewall"></a> 開啟防火牆通訊埠

開啟在標尺出主要安裝和連接埠的 SQL Server (1433，依預設)，指定的連接埠使用標尺出主要電腦上的 Windows 防火牆。
    
## <a name="Start"></a> 啟動 SQL Server 相應放大主機和背景工作服務

如果服務的啟動類型未設定為自動安裝期間，請啟動服務： SQL Server Integration Services 標尺出主要 14.0 (SSISScaleOutMaster140) 和 SQL Server Integration Services 標尺出工作者 14.0 (SSISScaleOutWorker140)。 

> [!Note]
> 開啟防火牆連接埠之後，您也需要重新啟動標尺出背景工作服務。
   
## <a name="EnableMaster"></a> 啟用相應放大主機

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)] 中建立 SSISDB 目錄時，請按一下 [建立目錄] 對話方塊中的 [啟用此伺服器作為 SSIS 相應放大主機]。 或者，可透過啟用標尺出主要[標尺出管理員](integration-services-ssis-scale-out-manager.md)之後建立的目錄。

## <a name="EnableAuth"></a> 啟用 SQL Server 驗證模式
如果[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]驗證未啟用資料庫引擎安裝期間，在上啟用 SQL Server 驗證模式[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]主控 SSISDB 目錄的執行個體。 

停用 SQL Server 驗證時，不會封鎖執行套件。 不過，執行記錄將無法寫入 SSISDB。

## <a name="EnableWorker"></a> 啟用相應放大背景工作

標尺出背景工作可透過啟用[標尺出管理員](integration-services-ssis-scale-out-manager.md)、 其提供 GUI; 或透過預存程序啟用，請參閱下方。

若要啟用相應放大背景工作，請執行將 *WorkerAgentId* 作為參數的 **[catalog].[enable_worker_agent]** 預存程序。 

向相應放大主機註冊相應放大背景工作之後，您會從 SSISDB 的 **[catalog].[worker_agents]** 資料庫檢視中取得 *WorkerAgentId* 值。 啟動相應放大主機和背景工作服務之後，註冊需要數分鐘的時間。

#### <a name="example"></a>範例
這個範例會啟用電腦 a 上出工作者小數位數。
```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName  --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    computerA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>後續的步驟
已完成相應放大功能設定。 您現在可以在向外執行封裝。如需詳細資訊，請參閱[在 Integration Services (SSIS) 相應放大中執行套件](run-packages-in-integration-services-ssis-scale-out.md)。

