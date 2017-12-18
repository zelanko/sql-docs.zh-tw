---
title: "逐步解說：設定 SQL Server Integration Services 相應放大 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ec9744a1efb0e78aca55e85e7f9f3eca007de5a2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="walkthrough-set-up-integration-services-scale-out"></a>逐步解說：設定 Integration Services 相應放大
完成下列工作，以設定 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 相應放大。 

> [!NOTE]
> 如果您要在一部電腦上安裝相應放大，請同時安裝相應放大主機和相應放大背景工作功能。 當您同時安裝這些功能時，會自動產生端點，以連接至相應放大主機。 

* [安裝相應放大主機](#InstallMaster)

* [安裝相應放大背景工作](#InstallWorker)

* [安裝相應放大背景工作用戶端憑證](#InstallCert)

* [開啟防火牆通訊埠](#Firewall)

* [啟動 SQL Server 相應放大主機和背景工作服務](#Start)

* [啟用相應放大主機](#EnableMaster)

* [啟用 SQL Server 驗證模式](#EnableAuth)

* [啟用相應放大背景工作](#EnableWorker)

## <a name="InstallMaster"></a> 安裝相應放大主機

若要啟用相應放大主機功能，您必須在設定 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 時安裝 Database Engine Services、[!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 和其相應放大主機功能。 

如需設定 Database Engine Services 和 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 的相關資訊，請參閱[安裝 SQL Server Database Engine](../../database-engine/install-windows/install-sql-server-database-engine.md) 和[安裝 Integration Services](../install-windows/install-integration-services.md)。
> [!NOTE]
> 若要使用預設 SQL 驗證帳戶進行相應放大記錄，請在資料庫引擎安裝期間，於 [資料庫引擎設定] 頁面上選取 [混合模式] 作為驗證模式。 如需詳細資訊，請參閱[變更相應放大記錄的帳戶](change-logdb-account.md)。

**若要安裝相應放大主機功能，請使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈或命令提示字元。**

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈的步驟
  1.  在 [特徵選取] 頁面上，選取列在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 下方的 [相應放大主機]。   
  ![特徵選取主機](media/feature-select-master.PNG)
  
  2.  在 [伺服器組態]  頁面上，選取要執行 [SQL Server Integration Services 相應放大主機服務]  的帳戶，然後選取 [啟動類型] 。  
  ![伺服器組態](media/server-config.PNG)
  3.  在 [Integration Services 相應放大主機組態]  頁面上，指定相應放大主機用來與相應放大背景工作通訊的通訊埠編號。 預設通訊埠編號是 8391。  
  ![Master 設定](media/master-config.PNG "Master 設定")
  4.  執行下列其中一項，以指定用來保護相應放大主機與相應放大背景工作間之通訊的 SSL 憑證。
    * 按一下 [建立新的 SSL 憑證]，讓安裝程序建立預設自我簽署 SSL 憑證。  預設憑證會安裝到 [受信任的根憑證授權單位] 的 [本機電腦] 下方。 您可以在此憑證中指定 CN。 主要端點的主機名稱應該併入 CN 中。 預設會包含 Master 節點的電腦名稱和 IP。
    * 按一下 [使用現有的 SSL 憑證]，然後按一下 [瀏覽] 選取憑證，以選取本機電腦上的現有 SSL 憑證。 憑證的指紋會出現在文字方塊中。 按一下 [瀏覽]  會顯示在 [受信任的根憑證授權單位] 的 [本機電腦] 中所儲存的憑證。 您選取的憑證必須儲存在這裡。       
![Master 設定 2](media/master-config-2.PNG "Master 設定 2")
  5.  完成 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈。
- 命令提示字元的步驟

    請遵循[從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 中的指示進行。 執行下列動作，以設定相應放大主機相關參數。
  1.  將 IS_Master 新增至 /FEATURES 參數
  2.  指定下列參數和其值來設定相應放大主機：/ISMASTERSVCACCOUNT、/ISMASTERSVCPASSWORD、/ISMASTERSVCSTARTUPTYPE、/ISMASTERSVCPORT、/ISMasterSVCSSLCertCN (選擇性)、/ISMASTERSVCTHUMBPRINT (選擇性)。

> [!Note]
> 如果相應放大主機未與資料庫引擎一起安裝，而且資料庫引擎是一個具名執行個體，則您需要在安裝之後於相應放大主機服務設定檔中設定 SqlServerName。 如需詳細資料，請參閱[相應放大主機](integration-services-ssis-scale-out-master.md)。

## <a name="InstallWorker"></a> 安裝相應放大背景工作
 
若要啟用相應放大背景工作功能，您必須在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝時安裝 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 和其相應放大背景工作功能。

**若要安裝相應放大背景工作功能，請使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈或命令提示字元。**

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈的步驟
  1.  在 [特徵選取] 頁面上，選取列在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 下方的 [相應放大背景工作]。   
  ![特徵選取背景工作](media/feature-select-worker.PNG)
  2. 在 [伺服器組態]  頁面上，選取要執行 [SQL Server Integration Services 相應放大背景工作服務]  的帳戶，然後選取 [啟動類型] 。    
  ![伺服器設定 2](media/server-config-2.PNG "伺服器設定 2")
  3. 在 [Integration Services 相應放大背景工作組態]  頁面上，指定連接至相應放大主機的端點。 
      > [!Note]
      > 您可以在這裡略過背景工作節點設定 (步驟 3 和 4)，並在安裝之後使用[相應放大管理員](integration-services-ssis-scale-out-manager.md)建立相應放大背景工作與相應放大主機的關聯。

    - 針對**單一電腦**環境，同時安裝相應放大主機和相應放大背景工作時，即會自動產生端點。 
    - 針對**多部電腦**環境，端點包含已安裝相應放大主機之電腦的名稱或 IP，以及相應放大主機安裝期間所指定的連接埠號碼。    
   ![背景工作設定 1](media/worker-config.PNG "背景工作設定 1")    

  4. 針對**多部電腦**環境，指定用來驗證相應放大主機的用戶端 SSL 憑證。 針對**單一電腦**環境，不需要指定用戶端 SSL 憑證。 
  
     > [!NOTE]
     > 自我簽署相應放大主機所使用的 SSL 憑證時，需要在具有相應放大背景工作的電腦上安裝對應的用戶端 SSL 憑證。 如果您在 [Integration Services 相應放大背景工作設定] 頁面上提供用戶端 SSL 憑證的檔案路徑，則會自動安裝憑證；否則，您稍後必須手動安裝憑證。 
     
     按一下 [瀏覽]  找出憑證檔案 (*.cer)。 若要使用預設 SSL 憑證，請選取位於已安裝相應放大主機之電腦的 \<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn 下方的 SSISScaleOutMaster.cer 檔案。   
   ![背景工作設定 2](media/worker-config-2.PNG "背景工作設定 2")
  5. 完成 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈。
- 命令提示字元的步驟

    請遵循[從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 中的指示進行。 執行下列動作，以設定相應放大背景工作相關參數。
    1.  將 IS_Worker 新增至 /FEATURES 參數
    2. 指定下列參數和其值來設定相應放大背景工作：/ISWORKERSVCACCOUNT、/ISWORKERSVCPASSWORD、/ISWORKERSVCSTARTUPTYPE、/ISWORKERSVCMASTER (選擇性)、/ISWORKERSVCCERT (選擇性)。

 
## <a name="InstallCert"></a> 安裝相應放大背景工作用戶端憑證

在安裝相應放大背景工作期間，將會在電腦上自動建立和安裝背景工作憑證。 同時，會在 \<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn 下方安裝對應的用戶端憑證 SSISScaleOutWorker.cer。 若要讓相應放大主機驗證相應放大背景工作，您必須將此用戶端憑證新增至具有相應放大主機之本機電腦的根存放區。
  
若要將用戶端憑證新增至根存放區，請連按兩下 .cer 檔案，然後按一下 [憑證] 對話方塊中的 [安裝憑證]  。 即會顯示 [憑證匯入精靈]  。  

## <a name="Firewall"></a> 開啟防火牆通訊埠

在相應放大主機電腦上使用 Windows 防火牆，以開啟在相應放大主機安裝期間所指定的連接埠以及 SQL Server 的連接埠 (預設為 1433)。
    
## <a name="Start"></a> 啟動 SQL Server 相應放大主機和背景工作服務

如果在安裝期間未將服務的啟動類型設定為 [自動]，請啟動服務︰SQL Server Integration Services 相應放大主機 14.0 (SSISScaleOutMaster140) 和 SQL Server Integration Services 相應放大背景工作 14.0 (SSISScaleOutWorker140)。 

> [!Note]
> 在您開啟防火牆連接埠之後，也需要重新啟動相應放大背景工作服務。
   
## <a name="EnableMaster"></a> 啟用相應放大主機

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)] 中建立 SSISDB 目錄時，請按一下 [建立目錄] 對話方塊中的 [啟用此伺服器作為 SSIS 相應放大主機]。 或者，在建立目錄之後，可以使用[相應放大管理員](integration-services-ssis-scale-out-manager.md)啟用相應放大主機。

## <a name="EnableAuth"></a> 啟用 SQL Server 驗證模式
如果未在資料庫引擎安裝期間啟用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 驗證，請在裝載 SSISDB 目錄的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體上啟用 SQL Server 驗證模式。 

停用 SQL Server 驗證時，不會封鎖執行套件。 不過，執行記錄將無法寫入 SSISDB。

## <a name="EnableWorker"></a> 啟用相應放大背景工作

相應放大背景工作的啟用是透過提供 GUI 的[相應放大管理員](integration-services-ssis-scale-out-manager.md)，或透過預存程序，請參閱下方。

若要啟用相應放大背景工作，請執行將 *WorkerAgentId* 作為參數的 **[catalog].[enable_worker_agent]** 預存程序。 

向相應放大主機註冊相應放大背景工作之後，您會從 SSISDB 的 **[catalog].[worker_agents]** 資料庫檢視中取得 *WorkerAgentId* 值。 啟動相應放大主機和背景工作服務之後，註冊需要數分鐘的時間。

#### <a name="example"></a>範例
這個範例會在 computerA 上啟用相應放大背景工作。
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
已完成相應放大功能設定。 您現在可以在相應放大中執行套件。如需詳細資訊，請參閱[在 Integration Services (SSIS) 相應放大中執行套件](run-packages-in-integration-services-ssis-scale-out.md)。
